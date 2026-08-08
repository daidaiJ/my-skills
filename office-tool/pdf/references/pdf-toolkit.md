# PDF 确定性脚本工具包（融合自 pdf-toolkit）

## 确定性脚本工具包（融合自 pdf-toolkit）

融合自 bundled skill `pdf-toolkit`（origin: clawhub-mit0，许可证 MIT-0，上游 https://clawhub.ai/pdf）。提供 4 个确定性脚本，用于程序化的结构 PDF 操作。

依赖：pypdf、pdfplumber、reportlab（Python 库；pdfplumber 已在默认依赖中）。

| 脚本 | 用途 | 示例 |
|---|---|---|
| `scripts/extract.py` | 提取文本/表格 | `python scripts/extract.py doc.pdf --json` |
| `scripts/merge.py` | 合并多个 PDF（支持按页范围 manifest） | `python scripts/merge.py a.pdf b.pdf --out combined.pdf` |
| `scripts/split.py` | 按页范围拆分 PDF | `python scripts/split.py input.pdf --pages "1-3,7,10-12" --out out/` |
| `scripts/form_fill.py` | 填充 AcroForm 表单字段 | `python scripts/form_fill.py form.pdf data.json --out filled.pdf` |

要点：

- **extract**：输出 JSON（`pages`/`metadata`/`text`/`tables`），文本与表格均用 pdfplumber 保留列布局；表格可用 `--tables-strategy lines|text|explicit` 切换检测模式。扫描件无文本层，需先 OCR。
- **merge**：直接合并整文件，或用 manifest.json 指定页范围 `{"file": "a.pdf", "pages": "1-3,5,7-9"}`；页范围 1 基、逗号分隔、连字符为区间，省略 `pages` 表示整文件。
- **split**：页范围语法同 merge，每个区间写一个输出文件（`output_001.pdf`、`output_002.pdf`…）。
- **form_fill**：用 `pypdf` 的 `get_fields()` 发现字段、`update_page_form_field_values()` 填充；JSON 中未出现的字段保持不变；`--list-fields` 可枚举字段名；`/Btn` 复选框取导出值（常为 Yes/On/1）；仅 AcroForm，XFA 表单需 Adobe 工具；必要时用 `--clear-signatures` 清除签名。

从零生成 PDF 用 reportlab（`canvas` 或 `platypus`），参考 `references/reportlab.md`；pypdf 用法参考 `references/pypdf.md`。加密 PDF 只读；签名/验签不在范围内。
