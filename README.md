# FFmpegAudioPlayer
A audio player for Android.

# 开发背景
Android MediaPlayer 所支持的音频格式太少，与厂商的内置硬件解码有关。
而 ExoPlayer 的 Extractors 也仅仅为 14 个，需要自己扩充。
所以想基于使用 FFmpeg 开发出一款几乎万能的音频格式播放器。

# 参考
[FFmpeg](https://github.com/FFmpeg/FFmpeg) FFmpeg Github 镜像

[Oboe](https://github.com/google/oboe) 安卓高性能低延迟（OpenSL ES + AAudio）C++ 音频库

# 开发计划
库拥有者 Moriafly 这方面技术比较差，希望有大佬一起开发~，QQ 群：481740141 。

# 目标
1. 给播放器一个地址就能播放（暂时先支持本地，后续支持网络）
2. “全格式”，FFmpeg 支持的所有音频格式都要能播放
3. 支持 seek、getDuration、getCurrentPosition 等基本功能以及完成播放等回调