# テキスト&波形表示サンプル
> http://lukaprincic.si/development-log/ffmpeg-audio-visualization-tricks


``` sh
ffmpeg \
-i sample.wav \
-i jacket.png \
-i background.png \
-filter_complex "
 [0:a]showwaves=mode=line:s=1800x480:colors=#FF0000@0.5|#FFAA00@0.5:scale=sqrt[fg];
 [2:v]scale=1920x1080[v];
 [v]drawtext=text='Ca5':fontcolor=White@0.8:fontsize=96:font=Arvo:x=60:y=60[v2];
 [v2]drawtext=text='Sample.wav':fontcolor=White@0.8:fontsize=144:font=Arvo:x=60:y=180[bg];
 [1:v]scale=720x720[jacket];
 [bg][fg]overlay=format=auto:alpha=premultiplied:x=60:y=840[bgfg];
 [bgfg][jacket]overlay=format=auto:alpha=premultiplied:x=1140:y=60[out]" \
-map "[out]" \
-map 0:a \
-vcodec libx264 \
-pix_fmt yuv420p \
-b:a 256k \
-r:a 44100  \
-s hd1080 \
OUTPUT.mp4
```

動作イメージ:  
[![sample image](http://img.youtube.com/vi/rtGAhK3AAJ0/0.jpg)](http://www.youtube.com/watch?v=rtGAhK3AAJ0)