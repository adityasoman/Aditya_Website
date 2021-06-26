# Computational Design Works

## Run locally

```
hugo server -D
```

## Add new post

```
hugo new posts/my-first-post.md
```

### New post format

```
+++
title = ""
date = ""
author = ""
authorTwitter = ""
cover = ""
tags = ["", ""]
keywords = ["", ""]
description = ""
showFullContent = false
+++
```

## Build static pages

```
hugo -D
```

## Theme

The theme is set to [https://github.com/sidswork/hugo-theme-terminal](https://github.com/sidswork/hugo-theme-terminal)

### Upgrade the theme to the latest version

```
git submodule update --init
git submodule update --rebase --remote
```
