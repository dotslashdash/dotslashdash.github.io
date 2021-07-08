---
layout: post
title: How I Built This Blog
description: Details on the creating of this blog
summary: Details on the creation of this blog
tags: how-to, blog
---

### Clone the source repo
```
git clone https://github.com/ronv/colorie.git my-blog
cd my-blog
```

### Test out basic Docker functionality
```
docker run --rm --volume="$PWD/docs:/srv/jekyll/" \
-p 4000:4000 \
jekyll/jekyll:3.8.6
jekyll serve
```

[Reference Host Your Own Blog with Jekyll, Docker, and Github Pages (YouTube)](https://youtu.be/ZHQ3IwIL590)

### Create the Docker Compose file
```docker
services:
  jekyll-serve:
    image: jekyll/jekyll:3.8.6
    volumes:
      - './docs:/srv/jekyll'
    ports:
      - 4000:4000
    command: 'jekyll serve'
```

### Fix code block indentation bug
While writing this post I discovered that inside code blocks there was unneccessary whitespace on the first line. This was resolved with the following css fix:
```
.post pre code {
  border: none;
  padding-left: 0;
}
```

