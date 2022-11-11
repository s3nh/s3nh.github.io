---
layout: post
title: "TIL 20221111 - Clean image resizing process, short story"
categories: routine
author: "s3nh"
meta: "Things I've learned"
---

<a href="https://www.buymeacoffee.com/s3nh"><img src="https://www.buymeacoffee.com/assets/img/guidelines/download-assets-sm-1.svg" alt=""></a>

Very lazy day, but I decided to write something, which was crucial to my actual work with Stable Diffusion Fine tuning. 

data preparation prior to the training process is essential and necessary. whether you are trying to build a logistic regression model or do a fine tune stable diffusion.

As I flourished in the subject of Dreambooth, after a few trained models, I noticed that the results I get are not satisfactory. models return noise, and the resulting photos often look like caricatures.

And eureka! darkest under the lantern, I haven't verified the size of each photo, which makes me incompetent.
I thought about it in the first iterations, but somehow I never wanted to do it, I hoped that the solution I use is resistant to it. Nothing could be more wrong ...

Quick think about how to resize 30k photos without launching * .py or * .ipynb.
And it turns out quite straight.
Imagemagick saved my life, follow a few steps on how to resize entire folders, with the indication that it is deliberately overwriting existing photos.

``` 
sudo apt-get update
sudo apt-get install imagemagick 
```

```
export SIZE=512x512
export QUALITY=75
export FORMAT=png

mogrify -resize $SIZE -format $FORMAT -quality $QUALITY *.jpg
```


All opinions are my own.  
s3nh
