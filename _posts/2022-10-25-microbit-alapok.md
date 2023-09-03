---
title: "Micro:bit alapok - Python"
layout: post
date: 2022-10-25 21:50
tags: microbit python
categories: blog
description: Micro:bit alapok - Python
---
A [python.microbit.org](https://python.microbit.org) oldalon elérhető micro:bit Python Editor kifejezetten a szövegalapú kódolásban járatlanok számára készült.

## Hello World!

Egy új nyelven való programozás hagyományos módja az, hogy a számítógép azt mondja: "Hello, World!".

```python
from microbit import *

#egyszerű scrollozó szöveg kiírása
display.scroll("Hello World!")
```
![Hello World](/assets/images/microbit/helloworld.gif)