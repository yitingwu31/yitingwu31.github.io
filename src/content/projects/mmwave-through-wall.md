---
title: "mmWave Radar Through-Wall Sensing"
description: "An mmWave radar sensor that penetrates hard woodboard wall to count the number of people moving behind the wall."
pubDate: "May 2023"
link: "https://github.com/yitingwu31/mmwave-sensing"
heroImage: "/post_img.webp"
tags: ["wireless sensing", "sensors"]
hashtags: ["Matlab", "Radar-sensing", "FMCW", "K-means-clustering"]
---

This project aims at using an mmWave radar sensor to detect and count the number of people behind a wall. The radar signal is transceived by a TI xWR6843 mmWave sensor and recorded with mmWave Studio Tool. The raw data is processed with Matlab. 

This project includes sensor hardware familiarity, signal processing and basic clustering. The sensor's sampling frequency, chirp frequency, chirp bandwidth, etc. to fit the general resolution requirements within a medium-sized indoor classroom setting. Fourier transform is applied to infer distance and velocity information from the Doppler shift of the Frequency Modulated Continouus Waves. Filters and convolutions are also applied to the converted data to further acquire the desired resolution and target clusters. Finally, we used K-means clustering with Elbow Method as well as Finding Connected Components to detect the number of targets in the moving scene.

