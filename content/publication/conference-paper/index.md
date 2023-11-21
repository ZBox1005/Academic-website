---
title: 'Boosting Semi-Supervised Object Detection in Remote Sensing Images with Active Teaching'

# Authors
# If you created a profile for a user (e.g. the default `admin` user), write the username (folder name) here
# and it will be replaced with their full name and linked to their profile.
authors:
  - admin
  - Zengmao Wang
  - Bo Du

# Author notes (optional)
# author_notes:
#   - 'Equal contribution'
#   - 'Equal contribution'

date: '2023-10-01T00:00:00Z'
doi: ''

# Schedule page publish date (NOT publication's date).
publishDate: '2023-10-01T00:00:00Z'

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ['2']

# Publication name and optional abbreviated publication name.
publication: Submitted to *Geoscience and Remote Sensing Letters*
publication_short: Submitted to *Geoscience and Remote Sensing Letters(GRSL)*

abstract: The lack of object-level annotations is a main challenge for object detection in remote sensing images. Active learning and semi-supervised learning can improve the quality and quantity of annotations by identifying the most informative samples for annotation and exploring the knowledge from the unlabeled samples respectively. In this paper, we propose a novel semi-supervised object detection method with active teaching for remote sensing images named SSOD-AT by combining object-level pseudo labeling and informative active annotation with a teacher-student network. In the proposed method, a RoI Comparison module (RoICM) is designed based on the teacher-student framework to provide high-confident pseudo-labels of RoIs. Meanwhile, we also use the RoICM to identify the top-K uncertain images. Then a diversity criterion is adopted based on the object-level prototypes of different categories with the labeled images and the pseudo-labeled images to remove the redundancy in the top-K uncertain images for human labeling. The extensive experiments on two popular datasets DOTA and DIOR show that the proposed method outperforms the state-of-the-art methods.

# # Summary. An optional shortened abstract.
# summary: The lack of object-level annotations is a main challenge for object detection in remote sensing images. In this paper, we propose a novel semi-supervised object detection method with active teaching for remote sensing images named SSOD-AT by combining object-level pseudo labeling and informative active annotation with a teacher-student network.

tags: []

# Display this page in the Featured widget?
featured: true

# Custom links (uncomment lines below)
# links:
# - name: Custom Link
#   url: http://example.org

links:
  - icon: github
    icon_pack: fab
    name: Code
    url: https://github.com/ZBox1005/
  - icon: file-pdf
    name: PDF
    url: uploads/SSOD-AT.pdf

# url_pdf: 'SSOD-AT.pdf'
# url_code: 'https://github.com/wowchemy/wowchemy-hugo-themes'
# url_dataset: 'https://github.com/wowchemy/wowchemy-hugo-themes'
# url_poster: ''
# url_project: ''
# url_slides: ''
# url_source: 'https://github.com/wowchemy/wowchemy-hugo-themes'
# url_video: 'https://youtube.com'

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/pLCdAaMFLTE)'
  focal_point: ''
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
# projects:
#   - example

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
# slides: example
---

{{% callout note %}}
Click the _Cite_ button above to demo the feature to enable visitors to import publication metadata into their reference management software.
{{% /callout %}}

{{% callout note %}}
Create your slides in Markdown - click the _Slides_ button to check out the example.
{{% /callout %}}

Supplementary notes can be added here, including [code, math, and images](https://wowchemy.com/docs/writing-markdown-latex/).
