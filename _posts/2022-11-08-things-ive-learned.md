---
layout: post
title: "TIL 20221108 - pytorch, cpu and fp16. short story"
categories: routine
author: "s3nh"
meta: "Things I've learned"
---


Pytorch ```conv``` operation does not support ```fp16``` operations on cpu. 
Remember to always check for compability before spending time on specific task. 

I am just one step before deployment semantic segmentation task, 
starting to use  pytorch profiler to check for eventual bootlenecks. 

Spent some time on optimization, when just after switch to cpu,
perform ```model.half()``` , 
prediction  return errors. 


https://github.com/open-mmlab/mmdetection/issues/2951

It is new, this is  caused by my lack of awareness. 
Pytorch profiler as a next nice thing to write about. 


All opinions are my own.  
s3nh
