---
language:
- en
tags:
- stable-diffusion
- stable-diffusion-diffusers
- text-to-image
- art
- artistic
- diffusers
inference: true
license: creativeml-openrail-m
---

# Protogen_x3.4

Protogen was warm-started with [Stable Diffusion v1-5](https://huggingface.co/runwayml/stable-diffusion-v1-5) and fine-tuned on various high quality image datasets.
Version 3.4 continued training from [ProtoGen v2.2](https://huggingface.co/darkstorm2150/Protogen_v2.2_Official_Release) with added photorealism.

## Space

We support a [Gradio](https://github.com/gradio-app/gradio) Web UI:
[![Open In Spaces](https://camo.githubusercontent.com/00380c35e60d6b04be65d3d94a58332be5cc93779f630bcdfc18ab9a3a7d3388/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f25463025394625413425393725323048756767696e67253230466163652d5370616365732d626c7565)](https://huggingface.co/spaces/darkstorm2150/Stable-Diffusion-Protogen-webui)

### CompVis

[Download ProtoGen_X3.4.ckpt) (5.98GB)](https://huggingface.co/darkstorm2150/Protogen_x3.4_Official_Release/blob/main/ProtoGen_X3.4.ckpt)

### 🧨 Diffusers

This model can be used just like any other Stable Diffusion model. For more information,
please have a look at the [Stable Diffusion Pipeline](https://huggingface.co/docs/diffusers/api/pipelines/stable_diffusion).

```python
from diffusers import StableDiffusionPipeline, DPMSolverMultistepScheduler
import torch

prompt = (
"modelshoot style, (extremely detailed CG unity 8k wallpaper), full shot body photo of the most beautiful artwork in the world, "
"english medieval witch, black silk vale, pale skin, black silk robe, black cat, necromancy magic, medieval era, "
"photorealistic painting by Ed Blinkey, Atey Ghailan, Studio Ghibli, by Jeremy Mann, Greg Manchess, Antonio Moro, trending on ArtStation, "
"trending on CGSociety, Intricate, High Detail, Sharp focus, dramatic, photorealistic painting art by midjourney and greg rutkowski"
)

model_id = "darkstorm2150/Protogen_x3.4_Official_Release"
pipe = StableDiffusionPipeline.from_pretrained(model_id, torch_dtype=torch.float16)
pipe.scheduler = DPMSolverMultistepScheduler.from_config(pipe.scheduler.config)
pipe = pipe.to("cuda")

image = pipe(prompt, num_inference_steps=25).images[0]

image.save("./result.jpg")
```

![img](https://huggingface.co/datasets/patrickvonplaten/images/resolve/main/protogen/rswf5qk9be9a1.jpg)