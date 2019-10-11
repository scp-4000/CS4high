#

```
FFmpeg 開發（一）常用處理視頻命令
閱讀 3896
收藏 135
2017-02-09
原文連結：mp.weixin.qq.com
在即時音視頻中應用深度學習，你需要瞭解這些juejin.im
前言：FFmpeg是做音視頻開發的一個優秀的開源庫，
可以在不同平臺下編譯，能夠實現視頻採集、視頻格式轉化、視頻截圖、視頻添加浮水印、視頻切片、視頻錄製、視頻推流、更改音視頻參數功能等。
通過終端命令及開發時如何實現這些功能，本文做一整理記錄，以備不時之需。下麵共四組命令。

第一組

1.分離視頻音訊流

ffmpeg -i input_file -vcodec copy -an output_file_video　　//分離視頻流ffmpeg -i input_file -acodec copy -vn output_file_audio　　//分離音訊流

2.視頻解複用

ffmpeg –i test.mp4 –vcodec copy –an –f m4v test.264

ffmpeg –i test.avi –vcodec copy –an –f m4v test.264

3.視頻轉碼

ffmpeg –i test.mp4 –vcodec h264 –s 352*278 –an –f m4v test.264

//轉碼為碼流原始檔

ffmpeg –i test.mp4 –vcodec h264 –bf 0 –g 25 –s 352*278 –an –f m4v test.264 //轉碼為碼流原始檔

ffmpeg –i test.avi -vcodec mpeg4 –vtag xvid –qsame test_xvid.avi //轉碼為封裝文件

說明：-bf B幀數目控制，-g 關鍵幀間隔控制，-s 解析度控制

4.視頻封裝

ffmpeg –i video_file –i audio_file –vcodec copy –acodec copy output_file

5.視頻剪切

ffmpeg –i test.avi –r 1 –f image2 image-%3d.jpeg //提取圖片

ffmpeg -ss 0:1:30 -t 0:0:20 -i input.avi -vcodec copy -acodec copy output.avi //剪切視頻//-r 提取圖像的頻率，-ss 開始時間，-t 持續時間

6.視頻錄製

ffmpeg –i rtsp://192.168.3.205:5555/test –vcodec copy out.avi

7、利用ffmpeg視頻切片

主要把視頻源切成若干個.ts格式的視頻片段然後生成一個.m3u8的切片檔索引提供給html5的video做hls直播源

命令如下：

ffmpeg -i 視頻源位址 -strict -2 -c:v libx264 -c:a aac -f hls m3u8檔輸出位址

8、ffmpeg縮放視頻

假設原始視頻尺寸是 1080p（即 1920×1080 px，16:9），使用下面命令可以縮小到 480p：(ps:以下這個命令，據說違反微信平臺相關法律，蛋疼，用不了文字，只能用圖片了)



各個參數的含義：-i a.mov 指定待處理視頻的檔案名-vf scale=853:480 vf 參數用於指定視頻濾鏡，其中 scale 表示縮放，後面的數字表示縮放至 853×480 px，其中的 853px 是計算而得，因為原始視頻的寬高比為 16:9，所以為了讓目標視頻的高度為 480px，則寬度 = 480 x 9 / 16 = 853-acodec aac 指定音訊使用 aac 編碼。注：因為 ffmpeg 的內置 aac 編碼目前還是試驗階段，故會提示添加參數 “-strict -2” 才能繼續，儘管添加即可。又或者使用外部的 libfaac（需要重新編譯 ffmpeg）。-vcodec h264 指定視頻使用 h264 編碼。注：目前手機一般視頻拍攝的格式（封裝格式、檔案格式）為 mov 或者 mp4，這兩者的音訊編碼都是 aac，視頻都是 h264。out.mp4 指定輸出檔案名上面的參數 scale=853:480 當中的寬度和高度實際應用場景中通常只需指定一個，比如指定高度為 480 或者 720，至於寬度則可以傳入 “-1” 表示由原始視頻的寬高比自動計算而得。即參數可以寫為：scale=-1:480，當然也可以 scale=480:-1 



9、ffmpeg裁剪

有時可能只需要視頻的正中一塊，而兩頭的內容不需要，這時可以對視頻進行裁剪（crop），比如有一個豎向的視頻 1080 x 1920，如果指向保留中間 1080×1080 部分命令如下：ffmpeg -i 視頻源位址 -strict -2 -vf crop=1080:1080:0:420 視頻輸出位址（如：out.mp4）

其中的 crop=1080:1080:0:420 才裁剪參數，具體含義是 crop=width:height:x:y，其中 width 和 height 表示裁剪後的尺寸，x:y 表示裁剪區域的左上角座標。比如當前這個示例，我們只需要保留豎向視頻的中間部分，所以 x 不用偏移，故傳入0，而 y 則需要向下偏移：(1920 – 1080) / 2 = 420

10. 轉視頻格式

ffmpeng -i source.mp4 -c:v libx264 -crf 24 destination.flv

其中 -crf 很重要，是控制轉碼後視頻的品質，品質越高，檔也就越大。

此值的範圍是 0 到 51：0 表示高清無損；23 是預設值（如果沒有指定此參數）；51 雖然檔最小，但效果是最差的。

值越小，品質越高，但檔也越大，建議的值範圍是 18 到 28。而值 18 是視覺上看起來無損或接近無損的，當然不代表是資料（技術上）的轉碼無損。

第二組

1.ffmpeg 把檔當做直播推送至伺服器 (RTMP + FLV)

ffmpeg - re -i demo.mp4 -c copy - f flv rtmp://w.gslb.letv/live/streamid

2.將直播的媒體保存到本地

ffmpeg -i rtmp://r.glsb.letv/live/streamid -c copy streamfile.flv

3.將一個直播流，視頻改用h264壓縮，音訊改用faac壓縮，送至另一個直播伺服器

ffmpeg -i rtmp://r.glsb.letv/live/streamidA -c:a libfaac -ar 44100 -ab 48k -c:v libx264 -vpre slow -vpre baseline -f flv rtmp://w.glsb.letv/live/streamb

4.提取視頻中的音訊,並保存為mp3 然後輸出

ffmpeg -i input.avi -b:a 128k output.mp3

5. 將mp3轉為pcm

ffmpeg-iinput.mp3-fs16be-acodecpcm_s16beoutput.pcm

第三組

1.獲取視頻的資訊

ffmpeg -i video.avi

2.將圖片序列合成視頻

ffmpeg -f image2 -i image%d.jpg video.mpg

上面的命令會把目前的目錄下的圖片（名字如：image1.jpg. image2.jpg. 等...）合併成video.mpg

3.將視頻分解成圖片序列

ffmpeg -i video.mpg image%d.jpg

上面的命令會生成image1.jpg. image2.jpg. ...

支援的圖片格式有：PGM. PPM. PAM. PGMYUV. JPEG. GIF. PNG. TIFF. SGI

4.為視頻重新編碼以適合在iPod/iPhone上播放

ffmpeg -i source_video.avi input -acodec aac -ab 128kb -vcodec mpeg4 -b 1200kb -mbd 2 -flags +4mv+trell -aic 2 -cmp 2 -subcmp 2 -s 320x180 -title X final_video.mp4

5.為視頻重新編碼以適合在PSP上播放

ffmpeg -i source_video.avi -b 300 -s 320x240 -vcodec xvid -ab 32 -ar 24000 -acodec aac final_video.mp4

6.從視頻抽出聲音.並存為Mp3

ffmpeg -i source_video.avi -vn -ar 44100 -ac 2 -ab 192 -f mp3 sound.mp3

7.將wav文件轉成Mp3

ffmpeg -i son_origine.avi -vn -ar 44100 -ac 2 -ab 192 -f mp3 son_final.mp3

8.將.avi視頻轉成.mpg

ffmpeg -i video_origine.avi video_finale.mpg

9.將.mpg轉成.avi

ffmpeg -i video_origine.mpg video_finale.avi

10.將.avi轉成gif動畫（未壓縮）

ffmpeg -i video_origine.avi gif_anime.gif

11.合成視頻和音訊

ffmpeg -i son.wav -i video_origine.avi video_finale.mpg

12.將.avi轉成.flv

ffmpeg -i video_origine.avi -ab 56 -ar 44100 -b 200 -r 15 -s 320x240 -f flv video_finale.flv

13.將.avi轉成dv

ffmpeg -i video_origine.avi -s pal -r pal -aspect 4:3 -ar 48000 -ac 2 video_finale.dv

或者：

ffmpeg -i video_origine.avi -target pal-dv video_finale.dv

14.將.avi壓縮成divx

ffmpeg -i video_origine.avi -s 320x240 -vcodec msmpeg4v2 video_finale.avi

15.將Ogg Theora壓縮成Mpeg dvd

ffmpeg -i film_sortie_cinelerra.ogm -s 720x576 -vcodec mpeg2video -acodec mp3 film_terminate.mpg

16.將.avi壓縮成SVCD mpeg2

NTSC格式：

ffmpeg -i video_origine.avi -target ntsc-svcd video_finale.mpg

PAL格式：

ffmpeg -i video_origine.avi -target pal-dvcd video_finale.mpg

17.將.avi壓縮成VCD mpeg2

NTSC格式：

ffmpeg -i video_origine.avi -target ntsc-vcd video_finale.mpg

PAL格式：

ffmpeg -i video_origine.avi -target pal-vcd video_finale.mpg

18.多通道編碼

ffmpeg -i fichierentree -pass 2 -passlogfile ffmpeg2pass fichiersortie-2

19.從flv提取mp3

ffmpeg -i source.flv -ab 128k dest.mp3

第四組

1、將文件當做直播送至live

ffmpeg -re -i localFile.mp4 -c copy -f flv rtmp://server/live/streamName

2、將直播媒體保存至本地檔

ffmpeg -i rtmp://server/live/streamName -c copy dump.flv

3、將其中一個直播流，視頻改用h264壓縮，音訊不變，送至另外一個直播服務流

ffmpeg -i rtmp://server/live/originalStream -c:a copy -c:v libx264 -vpre slow -f flv rtmp://server/live/h264Stream

4、將其中一個直播流，視頻改用h264壓縮，音訊改用faac壓縮，送至另外一個直播服務流

ffmpeg -i rtmp://server/live/originalStream -c:a libfaac -ar 44100 -ab 48k -c:v libx264 -vpre slow -vpre baseline -f flv rtmp://server/live/h264Stream

5、將其中一個直播流，視頻不變，音訊改用faac壓縮，送至另外一個直播服務流

ffmpeg -i rtmp://server/live/originalStream -acodec libfaac -ar 44100 -ab 48k -vcodec copy -f flv rtmp://server/live/h264_AAC_Stream

6、將一個高清流，複製為幾個不同視頻清晰度的流重新發佈，其中音訊不變

ffmpeg -re -i rtmp://server/live/high_FMLE_stream -acodec copy -vcodec x264lib -s 640×360 -b 500k -vpre medium -vpre baseline rtmp://server/live/baseline_500k -acodec copy -vcodec x264lib -s 480×272 -b 300k -vpre medium -vpre baseline rtmp://server/live/baseline_300k -acodec copy -vcodec x264lib -s 320×200 -b 150k -vpre medium -vpre baseline rtmp://server/live/baseline_150k -acodec libfaac -vn -ab 48k rtmp://server/live/audio_only_AAC_48k

7、功能一樣，只是採用-x264opts選項

ffmpeg -re -i rtmp://server/live/high_FMLE_stream -c:a copy -c:v x264lib -s 640×360 -x264opts bitrate=500:profile=baseline:preset=slow rtmp://server/live/baseline_500k -c:a copy -c:v x264lib -s 480×272 -x264opts bitrate=300:profile=baseline:preset=slow rtmp://server/live/baseline_300k -c:a copy -c:v x264lib -s 320×200 -x264opts bitrate=150:profile=baseline:preset=slow rtmp://server/live/baseline_150k -c:a libfaac -vn -b:a 48k rtmp://server/live/audio_only_AAC_48k

8、將當前攝像頭及音訊通過DSSHOW採集，視頻h264、音訊faac壓縮後發佈

ffmpeg -r 25 -f dshow -s 640×480 -i video=”video source name”:audio=”audio source name” -vcodec libx264 -b 600k -vpre slow -acodec libfaac -ab 128k -f flv rtmp://server/application/stream_name

9、將一個JPG圖片經過h264壓縮迴圈輸出為mp4視頻

ffmpeg.exe -i INPUT.jpg -an -vcodec libx264 -coder 1 -flags +loop -cmp +chroma -subq 10 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -flags2 +dct8x8 -trellis 2 -partitions +parti8x8+parti4x4 -crf 24 -threads 0 -r 25 -g 25 -y OUTPUT.mp4

10、將普通流視頻改用h264壓縮，音訊不變，送至高清流服務(新版本FMS live=1)

ffmpeg -i rtmp://server/live/originalStream -c:a copy -c:v libx264 -vpre slow -f flv “rtmp://server/live/h264Stream live=1〃


```
