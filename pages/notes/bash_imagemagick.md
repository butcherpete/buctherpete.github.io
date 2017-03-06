---
title: ImageMagick 
tags: [bash]
keywords:  
last_updated: February 17, 2017
summary: A list of essential command line skills for onboarding operations team members.
sidebar: notes_sidebar
permalink: bash_imagemagick.html
folder: notes 
---


[Save time by transforming images in the command line](https://hackernoon.com/save-time-by-transforming-images-in-the-command-line-c63c83e53b17#.vtvqpuaid)


Two key commands:

- Use `convert` change formats, resize, blur, crop, despeckle, dither, draw on, flip, join, and re-sample images.
- Use `mogify` to convert in place. The original file is overwritten unless you append the `-format` option to the file suffix. 

In general, use `mogrify` to modify multiple files and `convert` to modify a single file at a time.

> `convert` has a bug that makes it ignore one of the settings I recommend using (the `-define jpeg:fancy-upsampling=off` setting), so using `mogrify` is better.

## Resizing and Aspect Ratios

The `convert` and `mogrify` commands take the `-resize` argument.

```
# resize to 50%
$ mogrify -resize 50% *.jpg 

# resize, keep original aspect ratio
$ mogrify -resize 1024x768 *.jpg 

# resize, enforce exact dimensions
$ mogrify -r 1024x768! *.jpg 

# resize to width of 1024
$ mogrify -r 1024 

# resize to height of 1024
$ mogrify -r x768 *.jpg 
$ convert source.jpg -r 1024x768 output.jpg
```

## Cropping Images

To crop a 100x100 pixel range from the center of an image:

~~~
$ convert source.jpg -crop 100x100+0+0 -gravity center output.jpg
~~~

To crop the border from the edge of an image use the `shave` command.

~~~
#  shave 10px from sides
$ convert source.jpg -shave 10x10 output.jpg 
~~~

## Trimming Whitespace

To trim whitespace from images:

~~~
$ mogrify -trim *.{jpg,png}

# Use -fuzz to remove 'pixel residue'
$ mogrify -trim -fuzz 40% *.{jpg,png}
~~~

## Replacing Colors and Transparencies

To change colors in images:

~~~
$ convert white.png -fill '#000' -opaque '#fff' black.png
~~~

Use the `-fuzz` command to add tolerance.


To make a background transparent:

~~~
$ convert source.jpg -transparent white output.png
~~~


## Creating Favicons

To convert a source image into an ico:

~~~
$ convert source.png -define icon:auto-resize favicon.ico
~~~

The source image must be at least 256x256.

## Compression

[Efficient Image Resizing With ImageMagick](https://www.smashingmagazine.com/2015/06/efficient-image-resizing-with-imagemagick/)

## Custom Shell Scripts

Add scripts to the `~/.bash_profile`.


### Rename File Script

A script to rename image files using sequential numbers:

~~~
# Call with mv_seqnum

mv_seqnum(){
  a=1
  for i in $@; do
    new=$(printf "%04d.jpg" "$a")
    mv -- "$i" "$new"
    let a=a+1
  done
}
~~~

### Thumbnail Script

To create image sizes and folders for thumbnails and srcsets: 

~~~
# Call with img_size_folder thumbnail 150 

img_size_folder(){
  mkdir $1
  cp *.jpg $1
  cd $1
  mogrify -r $2 *.jpg
  cd ..
}
~~~

The example create a subfolder named "thumbnail", creates a copy of the image, and resizes those copies to 150px wide.


### Muliple Image Version Script

To create multiple versions of image versions:

~~~
# Call with $ create_image_sizes

create_image_sizes(){
  mv_seqnum
  img_size_folder big 1620
  img_size_folder full 1920
  img_size_folder medium 1024
  img_size_folder small 450
}
~~~

The command creates four folders (big, full, medium, and small) and adds appropriately sized copies of the image to each folder.

### Image Script

The script provides results that are comparable to the Photoshop "Save for the Web" function.

~~~
# Call with $ smartresize inputfile.png 300 outputdir/

smartresize() {
   mogrify -path $3 -filter Triangle -define filter:support=2 -thumbnail $2 -unsharp 0.25x0.08+8.3+0.045 -dither None -posterize 136 -quality 82 -define jpeg:fancy-upsampling=off -define png:compression-filter=5 -define png:compression-level=9 -define png:compression-strategy=1 -define png:exclude-chunk=all -interlace none -colorspace sRGB $1
}
~~~

The same script ported to GraphicsMagick:

~~~
gmsmartresize() {

gm mogrify -filter Triangle -define filter:support=2 -thumbnail $2 -unsharp 0.25x0.08+8.3+0.045 -dither -quality 82 -define jpeg:fancy-upsampling=off -define png:compression-filter=5 -define png:compression-level=9 -define png:compression-strategy=1 -define png:exclude-chunk=all -interlace none -strip -output-directory $3 $1
~~~

}
