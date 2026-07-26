---
name: self-verify
description: >
  Spawns a verifier subagent to audit your work: traces what was done, reviews
  the diff, runs builds/tests, and delivers a PASS/FAIL verdict. Auto-retries
  fixes up to 3 rounds. Use when asked to "check work", "verify changes",
  "self-verify", "/self-verify", "/check", or "/verify".
metadata:
  short-description: "Subagent-driven self-verification loop"
---

# /self-verify -- Self-Verification Loop

Spawn a verifier subagent that audits the current session's work, then fix
issues and re-verify until it passes (max 3 rounds).

## Usage

`/self-verify [focus area]`

Optional focus area tells the verifier what to pay special attention to
(e.g. "auth logic and JWT handling").

## Mode Detection

- **Same-turn mode**: A user task exists alongside this skill. **Complete the
  task fully first**, then proceed.
- **Standalone mode**: No pending task, just `/self-verify`. Proceed directly.

## Steps

1. Call the `agent` tool with:
   - `description`: start with `"[verifying my work]"` + short label
   - `subagent_type`: `"general-purpose"`
   - `run_in_background`: `false`
   - `prompt`: the **VERIFIER PROMPT** below verbatim. If a focus area was
     specified, append:
     ```
     ## Additional Focus
     <focus area text>
     Pay special attention to these areas during verification.
     ```

2. Look for `VERDICT: PASS` or `VERDICT: FAIL` in the result.

3. **PASS** -- summarize what was confirmed and stop.

4. **FAIL** -- fix the identified issues, then go back to step 1.
   Repeat up to 3 times. If still failing after 3 rounds, report the
   remaining issues to the user.

## VERIFIER PROMPT

You are an expert verifier. Your job is to determine whether the work done in
this session correctly and completely addresses the user's requests.

You already have the full conversation context, so you know what the user asked
for, what approach was taken, what tools were used, and what outcomes were
observed. You also have full access to the same environment and tools the
original agent had.

=== SCOPE ===

- If a **focus area** was specified, scope your verdict to that area but use
  the full session trace for context.
- If no focus area, verify **all work done in this session**.

=== WORKFLOW ===

Two phases. Phase A always runs. Phase B runs when the task involves code.

--- PHASE A: TRACE REVIEW ---

1. UNDERSTAND THE REQUEST:
   Restate everything the user asked for (all follow-ups, corrections,
   clarifications) as a concrete checklist. Include all task types: code,
   operational, git/PR, research, Q&A, configuration.

2. RECONSTRUCT WHAT HAPPENED:
   Trace every tool call and action. Look for:
   - Failed or unexpected outcomes
   - Requested items never attempted
   - Promised actions not actually done
   - Work deferred to the user that the agent could have done itself
   - Incorrect or incomplete answers
   - Reasoning errors

3. VERIFY CURRENT STATE:
   Inspect the environment yourself. Do not trust the conversation's claims:
   - Code changes? Read the modified files.
   - Commands run? Verify their effects.
   - Resources created (PRs, branches, configs)? Confirm they exist.
   - Questions answered? Check the source material.

--- PHASE B: CODE REVIEW ---

Skip this phase only if the session was purely non-code (general Q&A,
operational tasks with no code context, data analysis, research).

4. COLLECT THE DIFF:
   `git diff` (unstaged) + `git diff --cached` (staged) + `git log --oneline -3`
   + `git diff HEAD~1..HEAD` (recent commits). Read modified files and
   surrounding context.

5. EVALUATE THE CODE:
   - **Correctness**: Does it compile, run, pass tests? Broken build = FAIL.
   - **Adequacy**: Does it fully address the user's request?
   - **Excess**: Unnecessary refactors, unrelated changes, gold-plating?
   - **Edge Cases**: Sufficient coverage without over-engineering?

6. BUILD AND TEST:
   Read AGENTS.md / QWEN.md and README for build/test commands. Run them.
   Broken build or failing tests = automatic FAIL.

7. DESIGN AND RUN VERIFICATION CHECKS:
   Write your own tests or checks if needed. Exercise new functionality,
   check boundary conditions, confirm API effects. Thoroughness > speed.

8. REVIEW THE CODE:
   Look for: bugs, security issues, regressions, test quality (circular,
   over-mocked, happy-path-only), and project-instruction violations.

--- VERDICT ---

9. End with exactly one of:
   `VERDICT: PASS` -- work correctly and adequately addresses the user's requests
   `VERDICT: FAIL` -- issues need fixing (describe what, with file:line precision)

=== PRINCIPLES ===

- Verify outcomes, not just code. "Submit the eval job" means check the job
  was actually submitted, not just that the submission code is correct.
- Do not accept proxy signals. Passing tests are useful only if they cover
  every requirement.
- Do not invent issues. Genuine correctness deserves PASS. Style nitpicks
  that don't affect correctness should not cause FAIL.
- Violations of repo AGENTS.md / QWEN.md rules are policy, not nitpicks.
- Temporary test files you create for verification are fine.

=== OUTPUT FORMAT ===

## Checklist
Numbered list of all user requirements (code, operational, research, Q&A, etc.).

## Action Trace
For each checklist item: what was done, tools used, whether it succeeded.

## Diff Summary (Phase B only)
Files changed and scope.

## Evaluation (Phase B only)
- **Correctness**: compile/run/tests?
- **Adequacy**: request fully addressed?
- **Excess**: unnecessary changes?
- **Edge Cases**: sufficient coverage?

## Build & Test Results (Phase B only)
Exact command and result.

## Issues (skip if none)

### Issue N -- Severity: bug/gap/regression/suggestion
- File: path/to/file.ext:LINE
- Description: what is wrong
- Evidence: exact error or missing action
- Suggestion: how to fix

`VERDICT: PASS` or `VERDICT: FAIL`

## 闭卷知识验证 (ABC Loop) — 可选子流程

当被验证的产物是**文档 / Skill / 说明类知识**（而非直接可运行的代码改动）时，上面
的 VERIFIER PROMPT 侧重"工作是否完成"，但无法确认"该文档本身是否足以让一个
没读过源码的人准确理解"。此时启用借鉴自 `code-reader` 的 **ABC 闭卷验证回路**，
作为 self-verify 在知识沉淀场景下的增强。

### 适用场景

- 刚为某个陌生模块生成了 SKILL.md / 说明文档，想确认新人仅凭文档能否上手。
- 输出的架构白皮书、设计文档需要事实自洽性校验。
- 任何"以文档为交付物"的任务，在 PASS 之前追加一道闭卷检验。

### 三角色回路

- **A (Tech Writer / 作者)**：产出目标文档（SKILL.md / 说明等）。
- **B (QA Engineer / 出题人)**：**只阅读原始源码**（不读文档），针对文档应覆盖的
  关键事实生成 5–8 道验证题，每题附 `required_facts`（必须出现的事实点清单）。
- **C (Junior Dev / 闭卷作答人)**：**只阅读 A 的文档**（不读源码），逐题作答；
  无法从文档得出的题回答 `CANNOT_ANSWER`，不得猜测或编造。

### 评估与回填

主智能体（你）比对 C 的答案与 B 的 `required_facts`：

- 答案覆盖全部 `required_facts` → 该题 **PASS**；任一缺失 → **FAIL**。
- **硬性规则**：必须循环直到 100% 通过或满 3 轮，不得提前退出（99% 通过仍算失败）。
- 任一题 FAIL → 把"题目 + 答案要点 + C 的失败回答"回填给 A 重生成对应段落，
  再重跑 B 出题（携带历史题目避免重复）与 C 作答。
- 3 轮后仍有 FAIL → 把未通过题目与通过率呈现给用户判断，不得静默放过。

### 与 VERIFIER PROMPT 的关系

- VERIFIER PROMPT：验证"任务是否被正确、完整地完成"（过程与结果）。
- ABC Loop：验证"产物文档本身是否自洽、可被独立理解"（知识质量）。
- 两者可串联：先用 VERIFIER PROMPT 确认完成度，再视情况追加 ABC Loop 校验知识自洽性。

