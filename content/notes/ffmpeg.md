---
title: FFmpeg
slug: /ffmpeg
date: 2025-05-17
# draft: true
categories:
  - code
---

## WebM to mp3

```bash
ffmpeg -i vwMYtCgohX0.f251.webm -q:a 4 -vn brave.mp3
```

- `-i`：Input 輸入檔案
- `-q:a 4`：正常音質（quality, audio）
  - 0：最高音質，2：高音質，6：低音質
- `-vn`：不要輸出視訊（因為你只要音訊）

## 裁剪影片

```bash
ffmpeg -ss 00:39:50 -to 02:07:00 -i "20181223穿越的克里斯.mp4" -c copy "穿越的克里斯_裁切版.mp4"
```

| 參數   | 英文全名         | 中文解釋                         | 記憶小技巧                    |
| ------ | ---------------- | -------------------------------- | ----------------------------- |
| `-ss`  | **start time**   | 開始時間（從哪裡開始裁切）       | `ss = start seconds`          |
| `-to`  | **to time**      | 結束時間（到哪裡結束裁切）       | `to = 到哪裡為止`             |
| `-i`   | **input**        | 輸入檔案                         | `i = input`                   |
| `-c`   | **codec**        | 指定使用的編碼器                 | `c = codec`（編碼方式）       |
| `copy` | **copy streams** | 不重新壓縮，直接複製音訊與影片流 | `copy = 快速、省空間、不失真` |
