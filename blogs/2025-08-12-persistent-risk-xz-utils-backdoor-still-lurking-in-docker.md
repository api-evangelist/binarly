---
title: "Persistent Risk: XZ Utils Backdoor Still Lurking in Docker Images"
url: "https://www.binarly.io/blog/persistent-risk-xz-utils-backdoor-still-lurking-docker"
date: "2025-08-12"
feed_url: "https://www.binarly.io/blog/rss.xml"
---
In this blog, we share a new finding in the XZ Utils saga: several Docker images built around the time of the compromise contain the backdoor. At first glance, this might not seem alarming: if the distribution packages were backdoored, then any Docker images based on them would be infected as well. However, what we discovered is that some of these compromised images are still publicly available on Docker Hub.
