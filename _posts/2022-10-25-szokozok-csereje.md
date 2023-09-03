---
title: "Szóközök cseréje"
layout: post
date: 2022-10-25 10:37
tags: bash script linux
categories: blog
description: Szóközök cseréje
---

## Bash script:

```
#!/bin/bash

ls | while read -r FILE
do
    mv -v "$FILE" `echo $FILE | tr ' ' '_' `
done   

```
