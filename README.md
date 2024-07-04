# DiffSegX
## Exploring Diffusion Model for real image segmentation
Implementation is based on **prompt2prompt**: [Project Page](https://prompt-to-prompt.github.io)&ensp;&ensp;&ensp;[Paper](https://prompt-to-prompt.github.io/ptp_files/Prompt-to-Prompt_preprint.pdf)
> *Tuning method* and *Tuning free Method* Result

![tuning method](https://github.com/Scorbinwen/DiffSegX/assets/29889669/b2dc4dc3-72de-4a3a-9049-a630a2a6f757)
![tuning-free method](https://github.com/Scorbinwen/DiffSegX/assets/29889669/7c51f9e9-0ff4-4d06-a3ad-f5f8d0f512aa)

## Setup

This code was tested with Python 3.8, [Pytorch](https://pytorch.org/) 1.11 using pre-trained models through [huggingface / diffusers](https://github.com/huggingface/diffusers#readme).
Additional required packages are listed in the requirements file.
The code was tested on a Tesla V100 16GB but should work on other cards with at least **12GB** VRAM.

## Quickstart

In order to get started, we recommend taking a look at our notebooks: [**DiffSeg++**][diffseg++] and [**tuning_diff_seg**][tuning_diff_seg]. The notebooks contain end-to-end examples of usage of prompt-to-prompt on top of *Latent Diffusion* and *Stable Diffusion* respectively. Take a look at these notebooks to learn how to use the different types of prompt edits and understand the API.


# Tuning Method for DiffSegX
## Generate noise latent by tuning
generate noise latent for real image using method mentioned in: [Project Page](https://null-text-inversion.github.io/)&ensp;&ensp;&ensp;[Paper](https://arxiv.org/abs/2211.09794)

Null-text inversion enables intuitive text-based editing of **real images** with the Stable Diffusion model. We use an initial DDIM inversion as an anchor for our optimization which only tunes the null-text embedding used in classifier-free guidance.


## Aggregate CrossAttention Map
eDiff-I argues that crossAttion Map between query and key activates only in early sample steps, so we only sample for a few early steps, but actually what really spends time is in the tuning phase!
![image](https://github.com/Scorbinwen/DiffSegX/assets/29889669/70101c36-792a-47c5-ac8c-8c562c787a11)

# Tuning-Free Method for DiffSegX
## image vae latent sample
We use vae latent of image for aggregating crossAttention map, and we discovery that even in last few sample steps, crossAttion Map between query and key still matters:
![tuning-free method](https://github.com/Scorbinwen/DiffSegX/assets/29889669/7c51f9e9-0ff4-4d06-a3ad-f5f8d0f512aa)


## Disclaimer

This is not an officially supported Google product.

[diffseg++]: diffseg++.ipynb
[tuning_diff_seg]: tuning_diff_seg.ipynb
