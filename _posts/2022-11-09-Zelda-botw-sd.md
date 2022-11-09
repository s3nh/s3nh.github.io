---
license: creativeml-openrail-m
tags:
- stable-diffusion
- text-to-image
---

Buy me a coffee if you like this project ;)


<a href="https://www.buymeacoffee.com/s3nh"><img src="https://www.buymeacoffee.com/assets/img/guidelines/download-assets-sm-1.svg" alt=""></a>

Edit: Link to the project: https://huggingface.co/s3nh/zelda-botw-stable-diffusion

### Arcane based Artwork Diffusion Model

I present you fine tuned model of stable-diffusion-v1-5, which heavily based of 
work of great artworks from Legend of Zelda: Breath of The Wild.
Use the tokens **_botw style_** in your prompts for the effect.

Model was trained using the diffusers library, which based on Dreambooth implementation. 
Training steps included: 

- prior preservation loss
- train-text-encoder fine tuning 

### 🧨 Diffusers

This model can be used just like any other Stable Diffusion model. For more information,
please have a look at the [Stable Diffusion](https://huggingface.co/docs/diffusers/api/pipelines/stable_diffusion).

You can also export the model to [ONNX](https://huggingface.co/docs/diffusers/optimization/onnx), [MPS](https://huggingface.co/docs/diffusers/optimization/mps) and/or [FLAX/JAX]().

```python
#!pip install diffusers transformers scipy torch
from diffusers import StableDiffusionPipeline
import torch
model_id = "s3nh/s3nh/zelda-botw-stable-diffusion"
pipe = StableDiffusionPipeline.from_pretrained(model_id, torch_dtype=torch.float16)
pipe = pipe.to("cuda")
prompt = "Rain forest, botw style"
image = pipe(prompt).images[0]
image.save("./example_output.png")
```

# Gallery 

## Grumpy cat, botw style

<img src = "https://huggingface.co/s3nh/zelda-botw-stable-diffusion/resolve/main/grumpy cat0.png">

<img src = "https://huggingface.co/s3nh/zelda-botw-stable-diffusion/resolve/main/grumpy cat1.png">

<img src = "https://huggingface.co/s3nh/zelda-botw-stable-diffusion/resolve/main/grumpy cat2.png">

<img src = "https://huggingface.co/s3nh/zelda-botw-stable-diffusion/resolve/main/grumpy cat3.png">



## Landscape, botw style
![image](https://huggingface.co/s3nh/zelda-botw-stable-diffusion/resolve/main/landscape0.png)
![image](https://huggingface.co/s3nh/zelda-botw-stable-diffusion/resolve/main/landscape1.png)
![image](https://huggingface.co/s3nh/zelda-botw-stable-diffusion/resolve/main/landscape2.png)
![image](https://huggingface.co/s3nh/zelda-botw-stable-diffusion/resolve/main/landscape3.png)


All opinions are my own. 
S3nh
