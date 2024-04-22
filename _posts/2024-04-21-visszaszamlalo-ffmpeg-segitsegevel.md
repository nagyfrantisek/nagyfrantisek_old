---
title: "Visszaszámláló ffmpeg segítségével"
layout: post
date: 2024-04-21 13:47
tags: script bash 
categories: blog
description: Visszaszámláló ffmpeg segítségével
---


## Visszaszámláló 1 óra:

```
ffmpeg -loop 1 -i background.png -c:v libx264 -r 1 -t 3600 -pix_fmt yuv420p -vf "fps=1,drawtext=fontfile='./font.otf':fontcolor=black:fontsize=300:x=(w-text_w)/2:y=(h-text_h)/2:text='%{eif\:(mod((3600-t)/3600, 60))\:d\:2}\:%{eif\:(mod((3600-t)/60, 60))\:d\:2}\:%{eif\:(mod(3600-t, 60))\:d\:2}'" "1_hour_countdown.mp4"
```