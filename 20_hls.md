# HTTP Live Streaming (HLS)

`HLS` — протокол для потоковой передачи медиа (аудио/видео), на основе `HTTP`.

В основе работы лежит принцип разбиения цельного потока на небольшие фрагменты, последовательно скачиваемые по `HTTP`.

В начале сессии скачивается плей-лист в формате `.m3u8` (обычные текстовый файл), содержащий метаданные об имеющихся вложенных потоках.

Сами потоки находятся в файлах с расширением `.ts`.

Видео обычно кодируется с помощью `H264/h265`, аудио `AAC`.

[Ссылка на статью](https://developer.apple.com/library/content/referencelibrary/GettingStarted/AboutHTTPLiveStreaming/about/about.html)


## Конвертация (подготовка файлов для стриминга) `.mp4` в `.m3u8` и `.ts`

### FFMPEG

1. Скачиваем и устанавливаем [FFMPEG](http://www.ffmpeg.org/download.html).
У многих возникает вопрос как установить FFMPEG на Windows, поэтому ответ на этот вопрос можно найти [по ссылке](https://windowsloop.com/install-ffmpeg-windows-10/).
2. Прописываем `FFMPEG` в `PATH`.
3. Переходим в папку с видео:

   ```bash
   cd video_folder_name/
   ```

4. Создаем папки под видео:

   ```bash
   mkdir 1080 720 406 270 180
   ```

5. Нарезаем видео:

   ```bash
   ffmpeg \
     -i video_name.mp4 \
     -s 1920x1080 -c:a aac -c:v libx264 -map 0 -f segment -segment_time 10 -segment_format mpegts -segment_list 1080/playlist-1080.m3u8 "1080/video_name-1080-%d.ts" \
     -s 1280x720 -c:a aac -c:v libx264 -map 0 -f segment -segment_time 10 -segment_format mpegts -segment_list 720/playlist-720.m3u8 "720/video_name-720-%d.ts" \
     -s 720x406 -c:a aac -c:v libx264 -map 0 -f segment -segment_time 10 -segment_format mpegts -segment_list 406/playlist-406.m3u8 "406/video_name-406-%d.ts" \
     -s 480x270 -c:a aac -c:v libx264 -map 0 -f segment -segment_time 10 -segment_format mpegts -segment_list 270/playlist-270.m3u8 "270/video_name-270-%d.ts" \
     -s 320x180 -c:a aac -c:v libx264 -map 0 -f segment -segment_time 10 -segment_format mpegts -segment_list 180/playlist-180.m3u8 "180/video_name-180-%d.ts"
   ```

   Аналогичная команда для cmd:

   ```bash
   ffmpeg ^
     -i video_name.mp4 ^
     -s 1920x1080 -c:a aac -c:v libx264 -map 0 -f segment -segment_time 10 -segment_format mpegts -segment_list 1080/playlist-1080.m3u8 "1080/video_name-1080-%d.ts" ^
     -s 1280x720 -c:a aac -c:v libx264 -map 0 -f segment -segment_time 10 -segment_format mpegts -segment_list 720/playlist-720.m3u8 "720/video_name-720-%d.ts" ^
     -s 720x406 -c:a aac -c:v libx264 -map 0 -f segment -segment_time 10 -segment_format mpegts -segment_list 406/playlist-406.m3u8 "406/video_name-406-%d.ts" ^
     -s 480x270 -c:a aac -c:v libx264 -map 0 -f segment -segment_time 10 -segment_format mpegts -segment_list 270/playlist-270.m3u8 "270/video_name-270-%d.ts" ^
     -s 320x180 -c:a aac -c:v libx264 -map 0 -f segment -segment_time 10 -segment_format mpegts -segment_list 180/playlist-180.m3u8 "180/video_name-180-%d.ts"
   ```

6. Делаем обложку (если обложка не предоставлялась дизайнером):

   ```bash
   ffmpeg -i video_name.mp4 -ss 00:00:00 -vframes 1 cover.jpg
   ```

   <details>
     <summary>Удобнее это делать, используя переменную с названием видео:</summary>

     ```bash
     video_name="название_видео"

     mkdir 1080 720 406 270 180

     ffmpeg
       -i $video_name.mp4 \
       -s 1920x1080 -c:a aac -c:v libx264 -map 0 -f segment -segment_time 10 -segment_format mpegts -segment_list 1080/playlist-1080.m3u8 "1080/$video_name-1080-%d.ts"
       -s 1280x720 -c:a aac -c:v libx264 -map 0 -f segment -segment_time 10 -segment_format mpegts -segment_list 720/playlist-720.m3u8 "720/$video_name-720-%d.ts"
       -s 720x406 -c:a aac -c:v libx264 -map 0 -f segment -segment_time 10 -segment_format mpegts -segment_list 406/playlist-406.m3u8 "406/$video_name-406-%d.ts"
       -s 480x270 -c:a aac -c:v libx264 -map 0 -f segment -segment_time 10 -segment_format mpegts -segment_list 270/playlist-270.m3u8 "270/$video_name-270-%d.ts"
       -s 320x180 -c:a aac -c:v libx264 -map 0 -f segment -segment_time 10 -segment_format mpegts -segment_list 180/playlist-180.m3u8 "180/$video_name-180-%d.ts"

     ffmpeg -i $video_name.mp4 -ss 00:00:00 -vframes 1 cover.jpg
     ```

     Аналогичная команда для cmd:

     ```bash
     SET video_name="название_видео"

     mkdir 1080 720 406 270 180

     ffmpeg
       -i %video_name%.mp4 ^
       -s 1920x1080 -c:a aac -c:v libx264 -map 0 -f segment -segment_time 10 -segment_format mpegts -segment_list 1080/playlist-1080.m3u8 "1080/%video_name%-1080-%d.ts" ^
       -s 1280x720 -c:a aac -c:v libx264 -map 0 -f segment -segment_time 10 -segment_format mpegts -segment_list 720/playlist-720.m3u8 "720/%video_name%-720-%d.ts" ^
       -s 720x406 -c:a aac -c:v libx264 -map 0 -f segment -segment_time 10 -segment_format mpegts -segment_list 406/playlist-406.m3u8 "406/%video_name%-406-%d.ts" ^
       -s 480x270 -c:a aac -c:v libx264 -map 0 -f segment -segment_time 10 -segment_format mpegts -segment_list 270/playlist-270.m3u8 "270/%video_name%-270-%d.ts" ^
       -s 320x180 -c:a aac -c:v libx264 -map 0 -f segment -segment_time 10 -segment_format mpegts -segment_list 180/playlist-180.m3u8 "180/%video_name%-180-%d.ts"

     ffmpeg -i %video_name%.mp4 -ss 00:00:00 -vframes 1 cover.jpg
     ```
   </details>

   На выходе получаем видео, раскиданное по папкам с нужным размером и разбитое на файлы `.ts`, манифесты `.m3u8` (содержащие метаинформацию о файлах для каждого размера) и обложку `cover.jpg`.

7. Создаем мастер файл для объединения всех манифестов `video-name.m3u8`:

   ```
   #EXTM3U
   #EXT-X-VERSION:3
   #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=3880000,RESOLUTION=1920x1080,CODECS="mp4a.40.2,avc1.77.30",CLOSED-CAPTIONS=NONE
   1080/playlist-1080.m3u8
   #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=1810000,RESOLUTION=1280x720,CODECS="mp4a.40.2,avc1.77.30",CLOSED-CAPTIONS=NONE
   720/playlist-720.m3u8
   #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=800000,RESOLUTION=720x406,CODECS="mp4a.40.2,avc1.77.30",CLOSED-CAPTIONS=NONE
   406/playlist-406.m3u8
   #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=600000,RESOLUTION=480x270,CODECS="mp4a.40.2,avc1.77.30",CLOSED-CAPTIONS=NONE
   270/playlist-270.m3u8
   #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=410000,RESOLUTION=320x180,CODECS="mp4a.40.2,avc1.77.30",CLOSED-CAPTIONS=NONE
   180/playlist-180.m3u8
   ```

## Стандартные размеры видео для HLS

* **180p** — 320x180px
* **270p** — 480x270px
* **406p** — 720x406px
* **720p** — 1280x720px
* **1080p** — 1920x1080px

Точки `p` — определяющие название файла, берутся от высоты видео.
