---
title: "The Minimal Sane Hugo Setup"
date: 2024-07-11T10:42:15-07:00
---

I've set this up a million times, always forget how it's done. Here's the
minimal Hugo setup, because they can't seem to article it themselves.

```
.
├── config.toml
├── content
│   └── posts
│       └── first-post.md
├── layouts
│   ├── _default
│   │   ├── baseof.html
│   │   └── home.html
│   └── posts
│       └── single.html
```

`config.toml` is empty. `layouts/_default/baseof.html` is the top-level
template. I have it like this:

```html
<!doctype html>
<html>
<head>
  <title>{{ block "title" . }}{{ end }}</title>
</head>
<body>
  {{ block "main" . }}
  {{ end }}
</body>
</html>
```

Then all sub-templates need to define "title" and "main". 

The top-level index page uses `layouts/_default/home.html`:

```html
{{ define "main" }}
hello, world
{{ end }}
```

You can do listing of posts or whatever here.

The individual posts use `layouts/posts/single.html`:

```html
{{ define "title" }}
  {{ .Title }}
{{ end }}

{{ define "main" }}
  <main>
    <h1>{{ .Title }}</h1>
    <div>
      {{ .Content }}
    </div>
  </main>
{{ end }}
```

I do more from here, but mostly just CSS stuff.

Hugo is great, but it would likely kill the maintainers to explain anything
simply.
