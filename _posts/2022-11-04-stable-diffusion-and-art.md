---
layout: post
title: "Stable diffusion and art - Beksinski style"
categories: routine
author: "s3nh"
meta: "Stable diffusion"
---


Edit: 2022-11-07


<a href="https://www.buymeacoffee.com/s3nh"><img src="https://www.buymeacoffee.com/assets/img/guidelines/download-assets-sm-1.svg" alt=""></a>


# Release
This model can be used just like any other Stable Diffusion model. For more information,
please have a look at the [Stable Diffusion](https://huggingface.co/docs/diffusers/api/pipelines/stable_diffusion).

You can also export the model to [ONNX](https://huggingface.co/docs/diffusers/optimization/onnx), [MPS](https://huggingface.co/docs/diffusers/optimization/mps) and/or [FLAX/JAX]().

```python
#!pip install diffusers transformers scipy torch
from diffusers import StableDiffusionPipeline
import torch
model_id = "s3nh/beksinski-style-stable-diffusion"
pipe = StableDiffusionPipeline.from_pretrained(model_id, torch_dtype=torch.float16)
pipe = pipe.to("cuda")
prompt = "Bus riding to school, beksinski style"
image = pipe(prompt).images[0]
image.save("./example_output.png")
```


I'm not passionate about art. I will never be passionate about art.
However, I have always been fascinated by the thought process that goes on in the artist's head,
especially in the case that we will describe today.
I am interested in the path followed by the tool, the mind, and it is interesting to me
frequent contrast of the artist's works and his approach to life in the real world.

The works of artists have the feature that after their departure / completion of work, they leave
endless possibilities when it comes to reflection.
Even in life, we can reflect on what would have happened.


The world is certainly composed of a very large number of random phenomena,
from a lot of noise, and entropy doesn't help us with that.
Nevertheless, curiosity sparkles in our everyday life more and more as time progresses.


We already know that diffusion models are what has been missing in deep learning for some time, a breakthrough. A breakthrough that allows us to move away from falling into the deep learning routine. There is this element of freshness that allows us to get away from asking ourselves the question 'when are the dopamine shots coming?' They are there, and they let you enjoy creating something interesting again.

This led me to ask what if?
What if we could describe the more common, routine, using
the hand of a master who was certainly Zdzisław Beksiński.

I link the history of the Beksiński family to those who are interested,

- [History of Beksinski family](https://theculturetrip.com/europe/poland/articles/the-tragic-story-of-zdzislaw-beksinski-the-artist-who-inspired-guillermo-del-toro/)

and I will quickly go to how I implemented this issue.


The open source world was kind to me and helped me make this case. The hype train used by diffusion models does not adversely affect my actions.

Diffusion models have their basis in the theory of thermodynamic imbalance,
and interested in math heavy elements, I encourage you to read


- [Original Paper](https://arxiv.org/abs/1503.03585)

- [honestly, the best explanation of diffusion models](https://lilianweng.github.io/posts/2021-07-11-diffusion-models/)

So I decided to fine tune stable-diffusion (v1.5) model on Zdzislaw Beksinski artwork,
using different artwork as an regularization models.
After using 2000 iterations, the model gives outstanding results that allow you to feast your eyes on.
I encourage you to watch.
Edit: I load this version of a model to huggingface, so it can be used if needed. 
model is converted to .ckpt with only ema part, so inference can be performed with ~10gb of vram 





### Bus riding to school, beksinski style 


![image](https://raw.githubusercontent.com/s3nh/s3nh.github.io/master/_assets/bus1.png)



![image](https://raw.githubusercontent.com/s3nh/s3nh.github.io/master/_assets/bus2.png)

# Car traffic, beksinski style


![image](https://raw.githubusercontent.com/s3nh/s3nh.github.io/master/_assets/_cartraffic.png)


![image](https://raw.githubusercontent.com/s3nh/s3nh.github.io/master/_assets/car_traffic.png)


![image](https://raw.githubusercontent.com/s3nh/s3nh.github.io/master/_assets/car_traffic2.png)



# Dog drinking coffe

More abstract example, but also interesting. 


![image](https://raw.githubusercontent.com/s3nh/s3nh.github.io/master/_assets/dog_drinking_coffee.png)



# Eating breakfast on sunny day


![image](https://raw.githubusercontent.com/s3nh/s3nh.github.io/master/_assets/ebsd.png)



![image](https://raw.githubusercontent.com/s3nh/s3nh.github.io/master/_assets/ebsd2.png)


Thanks to paperspace for giving an opportunity to fine tune that kind of model with relatively low costs. 
But more about @paperspace in further posts. 


All opinions are my own.
S3nh
