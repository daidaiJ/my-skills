# 媒体处理工具

音视频和图片处理工具，基于 ffmpeg 和 ImageMagick。

| Skill | 用途 |
|-------|------|
| [ffmpeg](./ffmpeg/) | 视频/音频处理：合并、裁剪、转码、提取帧/音频、GIF、字幕；内置视频合并（merge_videos.py）与字幕烧录（burn_subtitles.py）脚本 |
| [imagemagick](./imagemagick/) | 图片处理：调整大小、裁剪、格式转换、水印、合成、批处理 |
| [md2video-audio](./md2video-audio/) | Markdown 一键转带真人配音的 MP4 口播视频：Marp 渲染幻灯片 + Edge-TTS 语音合成；串行流水线（优化稿→展示稿→口播稿）带分页校验与降级方案 |

## 安装依赖

两个 skill 都需要系统级工具，安装方式如下：

### Windows

```bash
# ffmpeg（推荐用 scoop 或 choco）
scoop install ffmpeg
# 或
choco install ffmpeg

# ImageMagick（推荐用 scoop 或 choco）
scoop install imagemagick
# 或
choco install imagemagick
```

### macOS

```bash
brew install ffmpeg imagemagick
```

### Linux (Debian/Ubuntu)

```bash
sudo apt update
sudo apt install ffmpeg imagemagick
```

### 验证安装

```bash
ffmpeg -version
ffprobe -version
magick -version
```

三个命令都有输出即表示安装成功。

### md2video-audio 附加依赖

```bash
pip install edge-tts moviepy markdown
npm install -g @marp-team/marp-cli
```

注意：Edge-TTS 依赖微软非官方免费端点，仅供个人非商业用途，随时可能失效（详见 [md2video-audio/SKILL.md](./md2video-audio/SKILL.md)）。
