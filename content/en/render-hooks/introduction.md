---
title: Introduction
description: An introduction to Hugo's render hooks.
categories: [render hooks]
keywords: []
menu:
  docs:
    identifier: render-hooks-introduction
    parent: render-hooks
    weight: 20
weight: 20
---

When rendering markdown to HTML, render hooks override the conversion. Each render hook is a template, with one template for each supported element type:

- [Code blocks](/render-hooks/code-blocks)
- [Headings](/render-hooks/headings)
- [Images](/render-hooks/images)
- [Links](/render-hooks/links)

{{% note %}}
Hugo supports multiple [content formats] including markdown, HTML, AsciiDoc, Emacs Org Mode, Pandoc, and reStructuredText.

The render hook capability is limited to markdown. You cannot create render hooks for the other content formats.

[content formats]: /content-management/formats/
{{% /note %}}

For example, consider this markdown:

```text
[Hugo](https://gohugo.io)

![kitten](kitten.jpg)
```

Without link or image render hooks, this example above is rendered to:

```html
<p><a href="https://gohugo.io">Hugo</a></p>
<p><img alt="kitten" src="kitten.jpg"></p>
```

By creating link and image render hooks, you can alter the conversion from markdown to HTML. For example:

```html
<p><a href="https://gohugo.io" rel="external">Hugo</a></p>
<p><img alt="kitten" src="kitten.jpg" width="600" height="400"></p>
```

Each render hook is a template, with one template for each supported element type:

```text
layouts/
└── _default/
    └── _markup/
        ├── render-codeblock.html
        ├── render-heading.html
        ├── render-image.html
        └── render-link.html    
```

The template lookup order allows you to create different render hooks for each page [type], [kind], language, and [output format]. For example:

```text
layouts/
├── _default/
│   └── _markup/
│       ├── render-link.html
│       └── render-link.text.txt
├── books/
│   └── _markup/
│       ├── render-link.html
│       └── render-link.text.txt
└── films/
    └── _markup/
        ├── render-link.html
        └── render-link.text.txt
```

[kind]: /getting-started/glossary/#page-kind
[output format]: /getting-started/glossary/#output-format
[type]: /getting-started/glossary/#content-type

The remaining pages in this section describe each type of render hook, including examples and the context received by each template.