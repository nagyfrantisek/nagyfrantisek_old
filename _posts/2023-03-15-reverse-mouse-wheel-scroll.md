---
title: "Reverse Mouse Wheel scroll"
layout: post
date: 2023-03-15 08:45
tags: windows tutorial
categories: blog
description: Reverse Mouse Wheel scroll
---

Open Windows PowerShell in Administrator Mode an paste:

```
$mode = Read-host "How do you like your mouse scroll (0 or 1)?"; Get-PnpDevice -Class Mouse -PresentOnly -Status OK | ForEach-Object { "$($_.Name): $($_.DeviceID)"; Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Enum\$($_.DeviceID)\Device Parameters" -Name FlipFlopWheel -Value $mode; "+--- Value of FlipFlopWheel is set to " + (Get-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Enum\$($_.DeviceID)\Device Parameters").FlipFlopWheel + "`n" }
```

It will ask how do you like your mouse to scroll.

0 - Move up so you see contents below (Default Mode, Windows behavior)
1 - Move down so you can see contents above (Natural Mode, Mac behavior, reverse mode)

Restart your computer. 
