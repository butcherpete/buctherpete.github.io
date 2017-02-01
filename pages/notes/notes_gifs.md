---
title: Animated Gifs  Notes 
tags: [bash]
keywords: ffmeg, imagemagick 
last_updated: January 31, 2017
summary: Create GIF screencast using QuickTime, ffmpeg, and ImageMagick..
sidebar: notes_sidebar
permalink: notes_gifs.html
toc: false
folder: notes 
---

## Step 1: Capturing Video 

1. In QuickTime Player, select File > New Screen Recording.
2. Click the red button, drag to select an area of the screen to record, and press the start button.
3. Select File > Export > 1080p.
4. Save the file.

## Step 2: Converting MOVs to GIFs

```
$ movtogif input.mov out.gif
```

## Step 3: Sharing GIFs Using Dropbox

```
cp out.gif ~/Dropbox/Public/screenshots/Screencast-`date +"%Y.%m.%d-%H.%M"`.gif
```

## Displaying Raw Images
To display raw images stored in the repository:

```
![Alt Text](https://github.com/{user}/{repo}/raw/master/path/to/image.gif)
```

## Setting Up 

The script:

```
movtogif(){
    ffmpeg -i "$1" -vf scale=800:-1 -r 10 -f image2pipe -vcodec ppm - |\
    convert -delay 5 -layers Optimize -loop 0 - "$2"
}
```
