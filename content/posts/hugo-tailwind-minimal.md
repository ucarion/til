---
title: "Minimal Sane Hugo + TailwindCSS Setup"
date: 2024-07-11T11:18:38-07:00
---

Following on from the [Hugo minimal setup post](/hugo-minimal), to add
TailwindCSS you can just add this `package.json` setup:

```json
{
  "scripts": {
    "dev": "npm-run-all -p dev:*",
    "dev:hugo": "hugo server",
    "dev:tailwindcss": "tailwindcss -i index.css -o static/index.css --watch"
  },
  "dependencies": {
    "@tailwindcss/typography": "^0.5.13",
    "npm-run-all": "^4.1.5",
    "tailwindcss": "^3.4.4"
  }
}
```

Now `npm run dev` is your new `hugo server`. Your `tailwind.config.js` is:

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "layouts/**/*.html"
  ],
  theme: {
    extend: {},
  },
  plugins: [
    require('@tailwindcss/typography'),
  ],
}
```

You also need the CSS entrypoint, at `./index.css` (i.e. the top level):

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Modify your `layouts/_default/baseof.html` to use the new generated CSS:

```html
<!doctype html>
<html>
<head>
  <title>{{ block "title" . }}{{ end }}</title>
  <link rel="stylesheet" href="/index.css" />
</head>
<!-- ... -->
```

You can now start adding tailwindcss classes to your templates, and they'll get
added to `/static/index.css` where Hugo will serve them at `/index.css`.
