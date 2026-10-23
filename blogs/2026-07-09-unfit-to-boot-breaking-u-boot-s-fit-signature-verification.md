---
title: "Unfit to Boot: Breaking U-Boot's FIT Signature Verification"
url: "https://www.binarly.io/blog/unfit-to-boot-breaking-u-boots-fit-signature-verification"
date: "2026-07-09"
feed_url: "https://www.binarly.io/blog/rss.xml"
---
The Binarly Research team has identified six new security vulnerabilities within U-Boot’s FIT (Flattened Image Tree) Signature Verification mechanism, a critical component for maintaining the Root of Trust in firmware. These flaws, affecting stable releases dating back to v2013.07, range from denial-of-service (DoS) conditions to potential arbitrary code execution during the processing of untrusted FIT images. This blog post details the technical nature of these vulnerabilities, demonstrating how they can be exploited, and discusses the coordinated disclosure process with the U-Boot maintainer
