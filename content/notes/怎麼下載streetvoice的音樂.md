---
title: 怎麼下載 StreetVoice 的音樂？
slug: /download-streetvoice-music
date: 2025-05-22
categories:
  - code
---

## StreetVoice 怎麼播放音樂？

- 一首三分鐘的歌曲，會被拆成大約 10 秒一段的 `.ts` 檔案。
- 系統會產生一個 `.m3u8` 播放清單，裡面寫好每段音樂的順序。
- 播放器就會照著清單，一段一段把 `.ts` 播起來，聽起來就像一首完整的歌。    
- 我們可以使用 `ffmpeg`這個終端機工具，透過 `.m3u8` 把這些段落抓下來，接起來，就能下載整首歌了。

## 下載流程

1. 打開開發者工具，點選 Network，並在搜尋欄搜尋「`m3u8`」。
2. 播放音樂，這時候開發者工具應該會跳出一項。
3. 複製那一項的 Request URL，大概會長得像這樣：`https://akhls.streetvoice.com/xxx.m3u8`。
4. 在終端機輸入：

```bash
ffmpeg -headers "Referer: https://streetvoice.com/" -i "https://akhls.streetvoice.com/xxx.m3u8" -c copy "歌名.mp3"
```

* `-headers "Referer: https://streetvoice.com/"`：告訴瀏覽器，我是從 StreetVoice 上面下載的。

## m3u8 是什麼？

它裡面不包含「音樂檔案」，而是一個純文字的播放清單檔案，告訴系統要播放的音樂順序，以及每首音樂有多久。

簡單來說就像：

```
1. 歌曲長度 3 分鐘，播放檔案：周杰倫 - 楓.mp3
2. 歌曲長度 4 分鐘，播放檔案：kobasolo, 春茶 - Love letter.mp3
3. ...
```

稍微貼近真實情況的例子：

```
1. 歌曲長度 10.004900 秒，播放檔案：eTGgeuMAuxms7DtfjmuYo2.mp3.128khls.mp3-00001.ts
2. 歌曲長度 10.004900 秒，播放檔案：eTGgeuMAuxms7DtfjmuYo2.mp3.128khls.mp3-00002.ts
3. ...
```

實際打開某個 `.m3u8` 長這樣：

```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:11
#EXT-X-MEDIA-SEQUENCE:1
#EXTINF:10.004900,
eTGgeuMAuxms7DtfjmuYo2.mp3.128khls.mp3-00001.ts
#EXTINF:10.004900,
eTGgeuMAuxms7DtfjmuYo2.mp3.128khls.mp3-00002.ts
#EXTINF:10.004889,
eTGgeuMAuxms7DtfjmuYo2.mp3.128khls.mp3-00003.ts
#EXTINF:10.004900,
eTGgeuMAuxms7DtfjmuYo2.mp3.128khls.mp3-00004.ts

...

#EXT-X-ENDLIST
```
