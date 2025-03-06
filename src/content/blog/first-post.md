---
title: First post to see results
description: Checking to see if subroots work now
pubDate: Mar 05 2025
heroImage: /blog-placeholder-3.jpg
---

After some research, I think the fix was that I just needed to turn on static website hosting. It was suggested to also make the S3 bucket the custom origin of the related Cloudfront distribution, but I think I already did that part. Of course, that's what this test is checking. If it works, great! If it doesn't, I'll look further into making the S3 bucket the custom origin.

In the origin tab of the distribution, I can see that it already has the S3 bucket as a origin I added in the past. I can tell because not only is the origin name and domain the same as the bucket name, but it also says that the origin type is "S3," so with any luck, once I commit this change, the invalidation should go through and the subroots, namely the blog and about pages, should be accessable. 
