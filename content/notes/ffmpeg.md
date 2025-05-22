---
title: FFmpeg
slug: /ffmpeg
date: 2025-05-17
# draft: true
categories:
  - code
---

## mp4 to mp3

```bash
ffmpeg -i input.mp4 -q:a 0 -map a output.mp3
```

- `-i`：Input 輸入檔案
- `-q:a 0`：音質最好（quality, audio）
	- 0：最高音質 / 2：高音質 / 4：正常音質 / 6：低音質
- `-map a`：只選擇音訊（audio）

## wav to mp3

```bash
ffmpeg -i input.wav -c:a libmp3lame -b:a 192k output.mp3
```

## webm to mp3

```bash
ffmpeg -i vwMYtCgohX0.f251.webm -q:a 4 -vn brave.mp3
```

- `-i`：Input 輸入檔案
- `-q:a 4`：正常音質（quality, audio）
    - 0：最高音質，2：高音質，6：低音質
- `-vn`：不要輸出視訊（因為你只要音訊）

## 裁剪音樂

```bash
ffmpeg -ss 00:39:50 -to 02:07:00 -i "原影片.mp4" -c copy "剪輯完.mp4"
```

- `-ss`：start time，開始時間
- `-to`：to time，結束時間
- `-i`：input，你要輸入的檔案
- `-c`：codec，指定使用的編碼器
- `copy`：不重新壓縮讀取，直接複製整個音訊跟影片，並進行剪輯

不只可以用 `.mp4`，`.mp3` 等的音樂檔也可以用同樣格式。

## 下載 StreetVoice 音樂

[點此連結](../download-streetvoice-music)。

## 將所有 `.wma` 轉成 `.mp3`。

```bash
find . -iname '*.wma' -exec sh -c 'ffmpeg -i "$1" -q:a 0 "${1%.wma}.mp3"' sh {} \;
find . -iname '*.wav' -exec sh -c 'ffmpeg -i "$1" -q:a 0 "${1%.wav}.mp3"' sh {} \;
find . -iname '*.wav' -exec sh -c 'ffmpeg -i "$1" "${1%.wav}.mp3"' sh {} \;
```

- `find .`：`.` 代表當前目錄，`find` 會在這裡開始搜索。
- `-iname '*.wma'`：尋找所有擴展名為 `.wma` 的檔案，不區分大小寫。
- `-exec sh -c '...' sh {} \;`：對於每個找到的檔案，`find` 命令會執行指定的 `sh -c` 命令。這裡，`sh -c` 允許我們執行一個小的 shell 腳本。
- `"ffmpeg -i "$1" -q:a 0 "${1%.wma}.mp3"`：`$1` 是由 `find` 傳入的檔案路徑（`{}` 的位置），`${1%.wma}.mp3` 使用 shell 的參數替換功能來將檔案名的 `.wma` 替換為 `.mp3`。
- `-q:a 0`：這是 ffmpeg 的選項，用來指定最高的音質。


