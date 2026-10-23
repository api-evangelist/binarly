---
title: "VulHunt in Practice: Detecting a Remote Code Execution Vulnerability in rsync"
url: "https://www.binarly.io/blog/vulhunt-in-practice-detecting-a-remote-code-execution-vulnerability-in-rsync"
date: "2026-01-30"
feed_url: "https://www.binarly.io/blog/rss.xml"
---
We walk through writing a VulHunt rule to detect CVE-2024-12084, a heap-based buffer overflow in rsync. Starting from understanding the vulnerability's root cause, we build detection logic step by step — covering rule metadata, function scoping, annotation, order guarantees, and decompiler queries — culminating in a production-ready rule that pinpoints the exact vulnerable code path in stripped binaries.
