---
title: Image gallery
description: Create beautiful interactive image gallery using Markdown
date: 2024-07-10 00:00:00+0800
image: 2.jpg
---

Hugo theme Stack supports the creation of interactive image galleries using Markdown. It's powered by [PhotoSwipe](https://photoswipe.com/) and its syntax was inspired by [Typlog](https://typlog.com/).

To use this feature, the image must be in the same directory as the Markdown file, as it uses Hugo's page bundle feature to read the dimensions of the image. **External images are not supported.**


## Result

![Image 2](2.jpg)

### 日本旅行
{{< gallery >}}
![test](test.jpg)
{{< /gallery >}}

> Photo by [mymind](https://unsplash.com/@mymind) and [Luke Chesser](https://unsplash.com/@lukechesser) on [Unsplash](https://unsplash.com/)