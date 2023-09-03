---
title: "Fájlnevek kisbetűssé alakítása"
layout: post
date: 2022-10-13 13:47
tags: script bash linux
categories: blog
description: Fájlnevek kisbetűssé alakítása
---

## Bash script:

```
#!/bin/bash
for filename in *
do
   n=`echo $filename | tr '[:upper:]' '[:lower:]'`
   mv $filename $n
done    

```
