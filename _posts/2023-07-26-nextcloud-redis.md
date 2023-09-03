---
title: "Redis server for Nextcloud"
layout: post
date: 2023-07-26 18:51
tags: nextcloud redis selfhost
categories: blog
description: How to install Redis for Nextcloud
---

How to install Redis for Nextcloud on Ubuntu:

<pre><code class="language-js">sudo apt install redis-server</code></pre>

<pre><code class="language-js">sudo nano /etc/redis/redis.conf</code></pre>

Change bind ```127.0.0.1``` to ```bind 0.0.0.0```

<pre><code class="language-js">sudo service redis-server restart</code></pre>

<pre><code>sudo apt install php-redis</code></pre>

```
sudo systemctl status redis
```
Edit nextcloud's config.php, and add:
```
'memcache.local' => '\\OC\\Memcache\\Redis',
'memcache.distributed' => '\\OC\\Memcache\\Redis',
'filelocking.enabled' => 'true',
'memcache.locking' => '\\OC\\Memcache\\Redis',
'redis' =>
array (
'host' => 'localhost',
'port' => 6379,
'timeout' => 0.0,
),
```