---
layout: default
title: ffmpeg读书笔记
parent: wordpress
---

# ffmpeg读书笔记

## 目录

- [ffmpeg常用命令模板](#ffmpeg常用命令模板)
- [《ffmpeg从入门到精通》读书笔记](#ffmpeg从入门到精通读书笔记)
  - [前言](#前言)
  - [ch01 FFmpeg简介](#ch01-FFmpeg简介)
  - [ch02 FFmpeg工具使用基础](#ch02-FFmpeg工具使用基础)
  - [ch03 FFmpeg转封装](#ch03-FFmpeg转封装)
    - [3.1 MP4是跨平台最好的格式](#31-MP4是跨平台最好的格式)
      - [3.1.1 MP4格式标准介绍](#311-MP4格式标准介绍)
      - [moov容器](#moov容器)
      - [3.1.2 MP4分析工具](#312-MP4分析工具)
      - [3.1.3 demuxer](#313-demuxer)
      - [3.1.4 muxer](#314-muxer)
      - [FFmpeg CENC加密mp4文件](#FFmpeg-CENC加密mp4文件)
    - [3.2 视频文件转FLV](#32-视频文件转FLV)
      - [3.2.1 FLV格式标准介绍](#321-FLV格式标准介绍)
      - [3.2.2 FFmpeg转FLV参数](#322-FFmpeg转FLV参数)
      - [3.2.3 FFmpeg文件转FLV举例](#323-FFmpeg文件转FLV举例)
      - [3.2.4 FFmpeg生成带关键索引的FLV](#324-FFmpeg生成带关键索引的FLV)
      - [3.2.5 FLV文件格式分析工具flvparse](#325-FLV文件格式分析工具flvparse)
    - [3.3 视频文件转M3U8](#33-视频文件转M3U8)
    - [3.4 视频文件切片](#34-视频文件切片)
      - [3.4.1 -f segment](#341--f-segment)
      - [3.4.2 FFmpeg切片segment举例](#342-FFmpeg切片segment举例)
      - [3.4.3 FFmpeg使用ss与t参数进行切片](#343-FFmpeg使用ss与t参数进行切片)
    - [3.5 音视频文件音视频流抽取](#35-音视频文件音视频流抽取)
      - [3.5.1 抽取aac音频流](#351-抽取aac音频流)
      - [3.5.2 抽取H.264视频流](#352-抽取H264视频流)
      - [3.5.3 抽取H.265视频流](#353-抽取H265视频流)
    - [3.6 系统资源使用情况](#36-系统资源使用情况)
  - [ch04 FFmpeg转码](#ch04-FFmpeg转码)
    - [4.1 软编码H.264与H.265](#41-软编码H264与H265)
      - [4.1.1 x264编码参数](#411-x264编码参数)
      - [4.1.2 H.264编码举例](#412-H264编码举例)
    - [4.2 FFmpeg硬编解码](#42-FFmpeg硬编解码)
    - [6.3 FFmpeg生成画中画](#63-FFmpeg生成画中画)
    - [6.8 绿幕抠图合并](#68-绿幕抠图合并)
    - [6.12 倍速处理](#612-倍速处理)
      - [atempo音频倍速处理](#atempo音频倍速处理)
      - [setpts视频倍速处理](#setpts视频倍速处理)

## ffmpeg常用命令模板

```bash
#裁剪视频
ffmpeg -i 输入文件名 -ss 1:02:03 -t 持续时长 -c copy 输出文件名

#不解码改变容器格式
ffmpeg -i input.flv -vcodec copy -acodec copy output.mp4

#合并多段视频：需要额外的文本描述文件
```

# 《ffmpeg从入门到精通》读书笔记

## 前言

中文经典资料

- [雷霄骅](https://blog.csdn.net/leixiaohua1020 "雷霄骅")
- [罗索实验室](http://www.rosoo.net/ "罗索实验室")
- [chinaffmpeg](http://bbs.chinaffmpeg.com/ "chinaffmpeg")

## ch01 FFmpeg简介

ffmpeg命令行选项中`-i`指定输入文件名，`-f`指定输出文件的容器格式

## ch02 FFmpeg工具使用基础

`ffmpeg -i input.rmvb -vcodec mpeg4 -b:v 200k -r 15 -an output.mp4`中各选项意思是：以input为输入文件，将视频编码转换为mpeg4格式，视频码率转换为200kbit/s，视频帧率转换为15fps，转码后的文件中不包括音频

`ffprobe -of csv -show_packets input.flv`可配合excel绘制直方图，与Elecard StreamEye的可视化图基本相同

`ffplay -vf "subtitles=字幕文件.srt" output.mp4`可加载字幕

## ch03 FFmpeg转封装

### 3.1 MP4是跨平台最好的格式

#### 3.1.1 MP4格式标准介绍

概念：

- box
  - header
  - data
    1. 可以是纯数据
    2. 也可以是更多子box
- fullBox

MP4文件由许多个box和fullBox组成，fullBox是box的扩展，在header中增加8位version标志和24位的flags标志

下面介绍解析时所需关键信息

#### moov容器

moov至少包含以下三种atom中的一种

1. mvhd：存放未压缩过的影片信息的头容器
2. cmov：压缩过的影片信息容器（不常用）
3. rmra：参考电影信息容器（不常用）

#### 3.1.2 MP4分析工具

1. Elecard StreamEye
2. mp4box
3. mp4info

#### 3.1.3 demuxer

MP4的demuxer操作通常使用默认配置即可

#### 3.1.4 muxer

muxer的可选参数多一些

1. faststart：正常情况下ffmpeg生成moov是在mdat写完成之后再写入，可以通过选项`-movflags faststart`将移到前面。在互联网的视频点播中，如果希望MP4文件被快速打开，则需要将moov存放在mdat前面
2. `-movflags dash`可生成dash格式
3. `ffmpeg -re -i input.mp4 -c copy -movflags isml+frag_keyframe -f ismv Stream`可以发布ISML直播流

#### [FFmpeg CENC加密mp4文件](https://www.jianshu.com/p/ea0761f6aa04 "FFmpeg CENC加密mp4文件")

`ffmpeg -h muxer=mp4`能看到mp4封装器提供的选项

1. `encryption_scheme`：加密的方案，只支持cenc-aes-ctr。
2. `encryption_key`：加密key，128比特(16bytes)，格式使用16进制的表示。加密和解密的时候使用。
3. `encryption_kid`：加密key的标识，128比特(16bytes)，格式使用16进制的表示。加密时需要，解密不需要。具体作用尚未找到参考。

```
加密示例

ffmpeg -i julin_5s.mp4 -c:v copy -c:a copy -encryption_scheme cenc-aes-ctr -encryption_key 76a6c65c5ea762046bd749a2e632ccbb -encryption_kid a7e61c373e219033c21091fa607bf3b8 encryption.mp4

播放示例

ffplay encryption.mp4 -decryption_key 76a6c65c5ea762046bd749a2e632ccbb

解密示例

ffmpeg -decryption_key c7e16c4403654b85847037383f0c2db3 -i encryption.mp4 decryption.mp4
```

### 3.2 视频文件转FLV

FLV常用于网络的直播与点播。其封装格式均以FLVTAG的形式独立存在

#### 3.2.1 FLV格式标准介绍

1. FLV文件头
2. FLV文件内容

#### 3.2.2 FFmpeg转FLV参数

比较简单

#### 3.2.3 FFmpeg文件转FLV举例

内部的音频或者视频不符合标准时，会报错 Audio codec ac3 not compatible with flv 。为了解决这类问题，可以用`-acodec aac`将音频从ac3转换为aac或者mp3

#### 3.2.4 FFmpeg生成带关键索引的FLV

在网络点播中常用yamdi工具为关键帧建立索引，用FFmpeg同样也可以实现，使用选项`flvflags add_keyframe_index`

#### 3.2.5 FLV文件格式分析工具flvparse

### 3.3 视频文件转M3U8

M3U8主要以文件列表的形式存在，既支持直播又支持点播，尤其在Android、iOS等平台最为常用

常规的从文件转换HLS直播时，使用的参数如下

`ffmpeg -re -i input.mp4 -c copy -f hls -bsf:v h264_mp4toannexb output.m3u8`

其中`-bsf:v h264_mp4toannexb`将H.264转换为AnnexB标准的编码，常见于实时传输流。如果源文件为FLV、TS则不需要这个参数。生成HLS时还有一些参数可以设置

1. `-start_number 300`设置列表中的第一篇的序号为300
2. `-hls_time 10`控制转码切片长度为10秒钟**左右**一片
3. `-lhs_list_size 3`设置M3U8列表中只保留3个TS分片

### 3.4 视频文件切片

HLS切片只支持TS，还可以

1. 使用segment方式切片
2. 使用ss加上t参数进行切片

#### 3.4.1 -f segment

`ffmpeg -re -i input.mp4 -c copy -f segment output-%d.mp4`

#### 3.4.2 FFmpeg切片segment举例

1. `-segment_format mp4`执行切片文件的格式为mp4

`ffmpeg -re -i input.mp4 -c copy -f segment -segment_format mp4 output-%d.mp4 `

2. ffconcat格式常见于虚拟轮播等场景

- `-segment_list_type ffconcat -segment_list output.lst`将生成ffconcat格式的索引文件名output.lst
- `-segment_list_type csv -segment_list output.csv`
- `-segment_list_type m3u8 -segment_list output.m3u8`

3. `-reset_timestamps 1`使切片时间戳归零
4. `-segment_times 3,9,12`在第3、9、12秒进行切片

#### 3.4.3 FFmpeg使用ss与t参数进行切片
`ffmpeg -i input.mp4 -c copy -ss 9 -t 8 -output_ts_offset 7 output.mp4`

`output_ts_offset`用于指定输出文件的`start_time`

### 3.5 音视频文件音视频流抽取

#### 3.5.1 抽取aac音频流
`ffmpeg -i input.mp4 -vn -acodec copy output.aac`

#### 3.5.2 抽取H.264视频流
`ffmpeg -i input.mp4 -vcodec copy -an output.h264`

#### 3.5.3 抽取H.265视频流
`ffmpeg -i input.mp4 -vcodec copy -an -bsf hevc_mp4toannexb -f hevc output.hevc`

由于mp4中存储的视频数据并不是标准的annexb格式，所以需要将mp4的视频存储格式存储为annexb格式，输出的hevc格式可以直接使用播放器进行观看。

### 3.6 系统资源使用情况
封装转换占CPU低，编码转换占CPU高

## ch04 FFmpeg转码

### 4.1 软编码H.264与H.265

FFmpeg本身并不支持H.264的编码器，而是由第三方模块支持。由于OpenH264开源比较晚，所以x264最常用。通过`ffmpeg -h encoder=libx264`可以查看到所支持的像素色彩格式

#### 4.1.1 x264编码参数

见表4-1。设置参数后编码生成的文件可以通过一些外部协助工具进行查看，如Elecard、Bitrate Viewer、ffprobe等

#### 4.1.2 H.264编码举例

1. 编码器预设参数设置`-preset slower`

- ultrafast：最快
- superfast：超级快速
- veryfast：非常快速
- faster：稍微快速
- fast：快速
- medium：折中
- slow：慢
- slower：更慢
- veryslow：非常慢
- placebo：最慢

1. 使用tune参数调优H.264编码时，可以包含如下几个场景

- film：对视频的质量非常严格时使用该选项
- animation：动画
- grain：颗粒物很重，该选项适用于颗粒感很重的视频
- stillimage：用于静止画面比较多的视频
- psnr：提高峰值信噪比
- ssim：提高结构相似性
- fastdecode：快速解码
- zerolatency：零延迟，用于直播

1. profile与level设置
2. 控制场景切换关键帧插入参数sc_threshold
3. 内部参数x264opts
4. CBR恒定码率设置参数nal-hrd

### 4.2 FFmpeg硬编解码

### 6.3 FFmpeg生成画中画
`ffmpeg -re -i input.mp4 -vf "movie=sub.mp4,scale=480x320[test]; [in][test] overlay [out]" -vcodec libx264 output.flv`

执行完命令之后会将sub.mp4视频文件缩放成宽480、高320的视频，然后显示在视频input.mp4的坐标为(0,0)的位置。如果希望子视频显示在指定位置，则需要用到overlay中的x坐标与y坐标的内部变量，如下所示，其中`main_w`为主画面宽度、`main_h`为主画面高度

`ffmpeg -re -i input.mp4 -vf "movie=sub.mp4,scale=480x320[test]; [in][test] overlay=x=main_w-480:y=main_h-320 [out]" -vcodec libx264 output.flv`

以上两种视频画中画的处理均为静态位置处理，此外还可以配合正则表达式进行跑马灯式画中画处理，动态地改变子画面的x坐标与y坐标。如下所示，子视频将会从主视频的左侧开始渐入视频从左向右游动，效果如图6-11所示

`ffmpeg -re -i input.mp4 -vf "movie=sub.mp4,scale=480x320[test]; [in][test] overlay=x='if(gte(t,2), -w+(t-2)*20, NAN)':y=0 [out]" -vcodec libx264 output.flv`

### 6.8 绿幕抠图合并

`ffmpeg -i input.mp4 -i input_green.mp4 -filter_complex "[1:v]chromakey=Green:0.1:0.2[ckout];[0:v][ckout]overlay[out]" -map "[out]" output.mp4`

将`input_green.mp4`绿色背景中的人物抠出来，设置标签为ckout，将其铺在input.mp4上

### 6.12 倍速处理

ffmpeg对于倍速处理支持跳帧播放和不跳帧播放

#### atempo音频倍速处理

这个滤镜只有一个参数：`0.5<tempo<2`

1. 半速处理`ffmpeg -i -input.wav -filter_complex "atempo=tempo=0.5" -acodec aac output.aac`
2. 2倍速处理`ffmpeg -i -input.wav -filter_complex "atempo=tempo=2.0" -acodec aac output.aac`

#### setpts视频倍速处理

这个滤镜只有一个参数：expr。常见值见表6-7

1. 半速处理`ffmpeg -re -i input.mp4 -filter_complex "setpts=PTS*2" output.mp4`
2. 二倍速处理`ffmpeg -i input.mp4 -filter_complex "setpts=PTS/2" output.mp4`

