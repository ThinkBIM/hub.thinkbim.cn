---
title: 使用 PHP-FFMpeg 操作视频/音频文件
date: 2021-07-29
description: 使用PHP-FFMpeg操作视频/音频文件
keywords: PHP|ffmpeg
tags:
  - ffmpeg 
  - PHP
categories:
  - PHP
top_img: false
cover: false
---

# 使用 PHP-FFMpeg 操作视频/音频文件



## 安装

```composer
composer require php-ffmpeg/php-ffmpeg
```

## 获取视频信息

```php

$url = "视频地址";

//参数配置
$mpegConf = [
  'ffmpeg.binaries' => env('ffmpeg.ffmpeg'), //ffmpeg bin目录
  'ffprobe.binaries' => env('ffmpeg.ffprobe'),//ffprobe bin目录
  'timeout' => 3600,
  'ffmpeg.threads' => 12
];
$ffmpeg = FFMpeg::create($mpegConf);
$video = $ffmpeg->open($url);
//视频的视频信I（width, height, duration）
$videoInfo = $video->getStreams()->videos()->first()->all();


Array
(
    [index] => 0
    [codec_name] => h264
    [codec_long_name] => H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10
    [profile] => High
    [codec_type] => video
    [codec_tag_string] => avc1
    [codec_tag] => 0x31637661
    [width] => 544
    [height] => 960
    [coded_width] => 544
    [coded_height] => 960
    [closed_captions] => 0
    [has_b_frames] => 1
    [pix_fmt] => yuv420p
    [level] => 31
    [color_range] => tv
    [color_space] => bt709
    [color_transfer] => bt709
    [color_primaries] => bt709
    [chroma_location] => left
    [refs] => 1
    [is_avc] => true
    [nal_length_size] => 4
    [r_frame_rate] => 30/1
    [avg_frame_rate] => 30/1
    [time_base] => 1/600
    [start_pts] => 0
    [start_time] => 0.000000
    [duration_ts] => 9000
    [duration] => 15.000000
    [bit_rate] => 1014409
    [bits_per_raw_sample] => 8
    [nb_frames] => 450
    [disposition] => Array
        (
            [default] => 1
            [dub] => 0
            [original] => 0
            [comment] => 0
            [lyrics] => 0
            [karaoke] => 0
            [forced] => 0
            [hearing_impaired] => 0
            [visual_impaired] => 0
            [clean_effects] => 0
            [attached_pic] => 0
            [timed_thumbnails] => 0
        )

    [tags] => Array
        (
            [creation_time] => 2021-04-14T01:27:05.000000Z
            [language] => und
            [handler_name] => Core Media Video
            [vendor_id] => [0][0][0][0]
        )

)

```



## 获取视频大小

```php


$mpegConf = [
  'ffmpeg.binaries' => env('ffmpeg.ffmpeg'),
  'ffprobe.binaries' => env('ffmpeg.ffprobe'),
  'timeout' => 3600,
  'ffmpeg.threads' => 12
];
$ffprobe = FFProbe::create($mpegConf);
$videoInfo = $ffprobe->format($remotefilename)->all();

//获取视频大小
$size = $ffprobe->format($remotefilename)->get('size');
//获取视频时长
$duration = $ffprobe->format($remotefilename)->get('duration');

//! ---------videoInfo--------
Array
(
    [filename] => /Desktop/1618363630035895.mp4
    [nb_streams] => 2
    [nb_programs] => 0
    [format_name] => mov,mp4,m4a,3gp,3g2,mj2
    [format_long_name] => QuickTime / MOV
    [start_time] => 0.000000
    [duration] => 15.000000
    [size] => 2018388
    [bit_rate] => 1076473
    [probe_score] => 100
    [tags] => Array
        (
            [major_brand] => mp42
            [minor_version] => 1
            [compatible_brands] => isommp41mp42
            [creation_time] => 2021-04-14T01:27:05.000000Z
            [copyright] => 
            [copyright-eng] => 
        )

)
```



## 视频截取

```php
//tempnam创建一个具有唯一文件名的临时文件
$localtempfilename = tempnam(ini_get('upload_tmp_dir'), 'hc-cover');
//截取视频，报错到临时文件
$video->frame(TimeCode::fromSeconds(0))->save($localtempfilename);
//给指定文件的内容生成哈希值
$videoCoverMd5 = hash_file('md5', $localtempfilename) . '_0.jpg';
```





[参考资料](https://blog.jam00.com/article/info/25.html)

