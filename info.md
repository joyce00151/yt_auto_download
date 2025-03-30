# YouTube 视频批量下载脚本使用说明
   本脚本使用yt-dlp从 YouTube 下载单个视频或合集中的视频，并将视频信息（原标题|中文标题|语言|分辨率|格式|发布日期|来源)保存为 CSV 文件。下载视频不会和已有视频重复，遇到重复的视频就跳过，下载列表中下一个视频。脚本支持网络错误重试、实时更新 CSV 文件、处理中断等功能。

## 运行环境配置
将脚本部署到新电脑上运行，需要确保以下配置：
* python库：
```txt
pip install yt-dlp selenium webdriver-manager googletrans==4.0.0-rc1 pandas
```
yt-dlp：用于下载 YouTube 视频。

selenium 和 webdriver-manager：用于自动获取 cookies。

googletrans：翻译视频标题。

pandas：读取和打印 CSV 文件内容。

* 安装FFmpeg：
必须安装 FFmpeg，用于合并视频和音频流，并将音频转换为 AAC 格式。

Windows：
1. 从 https://www.gyan.dev/ffmpeg/builds/ 下载 FFmpeg（例如 ffmpeg-6.0-essentials_build.zip）。
2. 解压到 C:/Program Files/ffmpeg-6.0-essentials_build。
3. 将 C:/Program Files/ffmpeg-6.0-essentials_build/bin 添加到系统环境变量 Path。
4. 运行 ffmpeg -version 确认安装成功。

* Edge 浏览器和驱动：
安装 Microsoft Edge 浏览器（脚本使用 Edge 获取 cookies）。

webdriver-manager 会自动下载 Edge 驱动，但需确保 Edge 浏览器已安装。
  
## 使用步骤
* 1.输入视频链接：

目前支持下载单个视频链接合集链接。修改脚本中的 playlist_url 变量：
```txt
playlist_url = "你的视频或合集链接"
```

* 2.运行脚本：

直接在python中运行或保存脚本为download_youtube.py后在命令行中运行：
```txt
python download_youtube.py
```

* 3.输出
* 视频文件

保存路径：D:/Videos（可通过 video_output_dir 修改）。

文件格式：[视频ID].mp4，例如 ocyu2uGneds.mp4。

* csv文件

保存路径：D:/Data/video_info.csv（可通过 csv_output_path 修改）。

内容：包含以下字段：原标题、中文标题、语言、分辨率、格式、发布日期、来源。

每次下载一个视频后更新，控制台会打印 CSV 内容

* 中断与恢复

按 Ctrl+C 中断程序，脚本会立即退出。

CSV 文件会保留已下载视频的信息，下次运行会跳过已下载的视频（通过 video_exists 检查）。

如果视频文件不完整，删除对应文件后重新运行，脚本会重新下载。
