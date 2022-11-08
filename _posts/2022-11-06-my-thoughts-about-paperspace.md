---
layout: post
title: "My thoughts about paperspace"
categories: routine
author: "s3nh"
meta: "Cloud Computing"
---

<a href="https://www.buymeacoffee.com/s3nh"><img src="https://www.buymeacoffee.com/assets/img/guidelines/download-assets-sm-1.svg" alt=""></a>

I am a big fan of implementing projects in my spare time.
I don't have too much of that last time, but I'm still trying not to drop out of the game.
And from this game it is not so much that you want, if you want to supplement your place on the RNN, and from some very important one, to do in a timely manner, or for example diffusion models.

Deep learning in 2022 is a resource-hungry success, and I have repeated opportunities over and over again.
how to tool itself specs for finished projects.
There are several possibilities in the search engine:

- rig station,  which allowed me to train model locally 
- Cloud computing services, which allows me to perform calculation on cloud (someone elses computer).


For a long time I often have to use Colab, Colab Pro, COlaba Pro +, and I accept all inconveniences it brought to the solution. I felt that the amount of added value was enough.
But after changes in Colab Policy (adding compute units for every instance), the disadvantages of the solution began to overtake its advantages. 
List only few of them:

- Lack of consistency of specification on every level of subscription
- Compute units consumption time is not clear at all, and if I understand correctly, not the  same for every user. 
- On Pro you still have to keep your session active, otherwise it will disconnect
- Terminal: it is great that it is possible to use it, but why it is so laggy?


### Time to change 

So yeah, it was not usable anymore, and also not so cheap. 
So after fast research I tried paperspace which suprised me with a list of free Tier gpu and subscription plan. 
Tried Pro plan, 8$ a month, seems pretty solid. I was really aware of potential additional costs, but there was not much of them. 
The only thing is, you have to be really careful about storage space if you do not want to pay much more than subscription payment. 


## First impression. 

Really clear jump straight to some semantic segmentation task. 
There are some predefined environments, which is nice (pytorch, huggingface, dall-e, etc, mostly focused on deeop learning projects).
Also terminals works pretty well, it is not laggy at all. 
So I have a feeling like I am writing a code on my private laptop. 
There are also possibilities of build an workflow, deploy a model as an api, 'just with a few clicks', which I ll describe in more details in the future. 

Interface is clear enough, everything seems to flow fluent, and there is no session disconnection after turning off you station, so it is usefuil. 
The only disadvantage which I am aware of is that instances can be borrowed for 6h only, max. 
It means that if you want to train something bigger at once, which requires many hours of training, it is not possible on Free Tiers Gpu. 
But it is doable on GPU with pricing option, which is solid. 

## Summarization 

Paperspace.com is a really good alternative for low budget computing machines, at the moment I jump straight to the Growth plan, 
which cost about 39$ monthly, but give me a nice vibe, and i do not have to worry about buying physical rig station. 
On growth plan there are Free tiers with A6000 48gb, A100 80gb, which can be really useful for hype trained task, like fine tuning stable diffusion. 


All opinions are my own. 
S3nh
