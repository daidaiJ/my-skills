# 媒体处理工具

音视频和图片处理工具，基于 ffmpeg 和 ImageMagick。

| Skill | 用途 |
|-------|------|
| [ffmpeg](./ffmpeg/) | 视频/音频处理：合并、裁剪、转码、提取帧/音频、GIF、字幕；内置视频合并（merge_videos.py）与字幕烧录（burn_subtitles.py）脚本 |
| [imagemagick](./imagemagick/) | 图片处理：调整大小、裁剪、格式转换、水印、合成、批处理 |

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
