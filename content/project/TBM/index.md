---
title: Machine Learning on TBMs Excavation
summary: A study of rock mass accurate classification based on multi-algorithm cross multi-feature optimization selection and TBM parameter efficient prediction using low-dimensional inputs.
tags:
  - Machine Learning
date: '2023-10-31T00:00:00Z'

# Optional external URL for project (replaces project detail page).
external_link: ''

image:
  caption: Photo by rawpixel on Unsplash
  focal_point: Smart

links:
  # - icon: twitter
  #   icon_pack: fab
  #   name: Follow
  #   url: https://twitter.com/georgecushen
  - icon: github
    icon_pack: fab
    name: Code
    url: https://github.com/ZBox1005/
  - icon: file-pdf
    name: PDF
    url: uploads/TBM-paper.pdf
  - icon: file
    name: Slides
    url: uploads/TBM.pptx
# url_code: ''
# url_pdf: 'content/project/example/paper.docx'
# url_slides: ''
# url_video: ''

authors:
  - Xinyue Zhang
  - Wenbo Zhang
  - admin
  - Xiaoping Zhang
author_notes:
  - 'Equal contribution'
  - 'Equal contribution'
  - 'Equal contribution'


# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
# slides: example
---
## Abstract

Tunnel boring machines (TBMs) often encounter diverse geological conditions and complex rock-machine interactions in the long-distance excavation. Adverse geological conditions can lead to reduced excavation efficiency and even engineering risks, such as machine jams. Therefore, the perception of geological conditions, and the optimization of operational parameters under geological variations are of vital significance for TBM excavation safety and efficiency. To address the above two issues, the present study utilizes TBM big data and machine learning algorithms to infer rock mass classes and machine mechanical responses. Firstly, for TBM big data preprocessing, a Score-Kneedle algorithm based on knee point detection is proposed to accurately divide TBM tunneling cycles. The effectiveness of this algorithm has been validated on the Ying Song tunnel project in Jilin. Compared to the most commonly used duration division method, the proposed algorithm significantly improved division accuracy from 74.5% to 91.6%. Subsequently, using this algorithm, the TBM tunneling cycles are divided into five phases, i.e., free rotating, free advancing, increasing, stable, and decreasing phases. Features are extracted from different stages for rock mass classification and parameter prediction. For rock mass classification, three input feature combinations are extracted from the increasing and stable phases and are cross-trained with seven different models, i.e., SVM, CART, RF, GBDT, MLP, CNN, and GANDALF. The training results indicate that, regardless of the feature combination used, the SVM model consistently ensures high and stable classification performance with an F1 score of 0.88 for the four-class classification and 0.90 for the binary classification, making SVM the benchmark model for rock mass classification. For parameter prediction, GANDALF-based models for single-cutter torque and single-cutter thrust prediction are proposed. These models efficiently predict TBM parameters using a minimal set of inputs (cutterhead rotation speed, advance speed, total thrust force/cutterhead torque). In comparison to the reference prediction accuracy provided by the proposition group, the GANDALF-based models improve the average goodness of fit (R2) for single-cutter torque from 0.7171 to 0.7615 and for single-cutter thrust from 0.5895 to 0.6691. This level of accuracy fulfills the requirements for intelligent prediction of TBM excavation parameters.
