---
layout: post
title: How I Built This Blog
description: Details on the creating of this blog
summary: Details on the creation of this blog
tags: how-to blog
---

### Clone the source repo
```
git clone https://github.com/ronv/colorie.git dotslashdash.github.io
cd dotslashdash.github.io
```

### Test out basic Docker functionality
Now we are going to get this blog up and running in Docker to verify the proof
of concept.
```
docker run --rm --volume="$PWD/docs:/srv/jekyll/" \
-p 4000:4000 \
jekyll/jekyll:3.8.6
jekyll serve
```
You can now browse this local copy at [http://localhost:4000](http://localhost:4000)

[Reference Host Your Own Blog with Jekyll, Docker, and Github Pages (YouTube)](https://youtu.be/ZHQ3IwIL590)

### Create the Docker Compose file
Instead of running manual Docker commands we will package this all into a
docker-compose.yml file:
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


I was inspired to create this blog after browsing [https://jayriverlong.github.io/](https://jayriverlong.github.io).
