# Video Generator from Prompt

## Description
Generate a video from a prompt.

## Inspiration
* [How AI Image Generators Work (Stable Diffusion / Dall-E) - Computerphile](https://www.youtube.com/watch?v=1CIpzeNxIhU)
* [Introduction to Diffusion Models for Machine Learning](https://www.assemblyai.com/blog/diffusion-models-for-machine-learning-introduction/)
* [Video Diffusion in PyTorch](https://github.com/lucidrains/video-diffusion-pytorch)
  * Drawn from Jonathon Ho's paper [Video Diffusion Models](https://arxiv.org/abs/2204.03458)

## Running the program

* Run all blocks in `load_gifs.ipynb`
* Run all blocks in `video_diffusion.ipynb`
  * Input the text for the generated video
  * The output will be saved to a gif named after the prompt given

## Process
* Our initial concept was to generate the first frame of the video with a GAN, then use a sequence to sequence model to create frames after the first
* When we learned about the more state-of-the art diffusion models, we decided to use one to generate the first frame
* We came across a paper on diffusion specifically for video generation, which inspired our final product

## The Model
* A 3-dimensional UNet model is used to denoise input frames
  * The first 2 dimensions are the width and height of the image, and the 3rd is time
  * Temporal attention is used, meaning that the input is boosted for certain time points during training, allowing the model to focus and learn on them
  * The model takes noisy frames and their timecode and outputs a denoised version of the video
* The model is trained on GIFs from Tumblr and their captions
  * The caption is embedded using a pretrained BERT model
  * Sometimes, the caption is ignored and replaced by the embedding for blank strings. This allows the model to learn how to generate realistic GIFs regardless of the caption

## Lessons Learned
We took on a very ambitious project to complete in a short amount of time. Since we did not have unlimited resources or time available, we could not train on a large dataset for a long time. For such a complex model, this led to outputs which were not ideal, and did not really represent the prompt given. It is important to consider realistic factors such as these when taking on a project.
