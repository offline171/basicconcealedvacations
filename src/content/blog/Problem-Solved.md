---
title: Problem Solved!
description: I finally got to the bottom of the subroot issue
pubDate: Mar 06 2025
heroImage: /blog-image-2.jpg
---

When I first opened the dev website today, I actually found that that problem wasn't solved! I was worried that I'd need help with this and would need to wait until the 7th to fix this over the phone with my uncle, but with just a little bit of tinkering in the distribution origins tab, I figured out the issue. 

When my uncle and I first made the original concealed vacations website, we did make the buckets run with the static website option enabled, but we didn't change the origin domain to be the website endpoint link distributions suggested because there was nothing wrong with how it ran normally. However, now that this version has multiple subroots, it's become clear that changing the origin domain to suit the static website layout is necessary to enable the subroots to be seen. TIL I suppose.
