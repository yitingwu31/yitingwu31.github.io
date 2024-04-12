---
title: "Efficient CUDA Circle Renderer"
description: "A simple image renderer with CUDA C++ to accelerate the compute speed of multi-layer circle graphs on GPUs"
pubDate: "Nov 2023"
# link: "https://github.com/yitingwu31/midi-chords"
heroImage: "/post_img.webp"
tags: ["Parallel Computing", "GPU Programming"]
hashtags: ["CUDA C++"]
---

Problem description can be found [here](https://github.com/stanford-cs149/asst3)

High efficient computation is crucial for modern applications like AI/ML and high-quality image generation. This project focuses on optimizing an image renderer that renders millions of overlapping semi-transparent circles. The project is written in CUDA C++ for computing on GPU. The code is run on AWS Lightsail.

Some key considerations on optimization includes:
- What workloads can be done in parallel
- How to achieve optimal data locality
- Reduce redundant computation

A crucial constraint of the problem is that due to the semi-transparency of the circles, we must render overlapping circles in their correct order. Another critical consideration is the enormous size of data points (number of circles and pixels) we must compute. To achieve optimization within the constraints, I took some incremental steps that include
1. Identify the circles that do not intercept, so we can render these in parallel later
    1. Break the image into blocks (eg. blocks of 16x16 pixels), and check what circles intersect with this block
    2. When checking intersection, use coarse-grained intersection by comparing the block with the bounding box of the circle. This substitutes multiplications with all additions/subtractions, and thus can achieve better efficiency without losing important information.
    3. Checking intersection can be done in block-level parallelism.
2. Render each pixel in parallel
    1. The work at each pixel is unrelated, so we can render circles at a pixel-level parallelism
    2. For each pixel, first use fine-grained intersection to check if the circle actually intersects with the pixel (since from the previous step, we only know if the circle overlaps with the block)
    3. In particular, when dispatching CUDA threads, we intentionally generate 2D block dimension, with block sizes the same as the block sizes used in step 1 to find intersection. With 2D block dimension, the pixel threads inside the same block will be accessing the same set of circles, hence, once we load the circle data into the block's shared cache, it is likely the data will be reused by other pixel threads and thus reduce cache capacity misses.
    4. I also paid special attention to replace any repeated pointer reference to value. That is, we want to load in an initial value of a pixel, render all the circles onto it, and then write the value back to the pixel, instead of calling the pixel repeatedly with pointer. This reduces memory access and saves a lot of time.

The report can be found [here](https://drive.google.com/file/d/1qfUK_NvOb94zBDc2ugq41yrXFQDTdHmT/view?usp=sharing)<br>
*Due to Stanford Honor Code, the code of class assignment project cannot be disclosed.*
