# Writing & Uploading Blog Posts

## Create a post

Add a file to `src/content/blog/`. The filename becomes the URL slug.

```
src/content/blog/my-post-title.md  →  peterbacalso.com/blog/my-post-title
```

## Frontmatter

Every post must start with:

```markdown
---
title: "Post Title"
description: "One sentence summary shown on the blog index."
pubDate: 2024-06-01
tags: ["ml", "python"]
---

Post content here...
```

`tags` and `updatedDate` are optional. All other fields are required.

## Draft posts

Add `draft: true` to hide a post from the listing without deleting it:

```markdown
---
title: "Work in Progress"
draft: true
...
---
```

## Publish

```bash
git add src/content/blog/my-post-title.md
git commit -m "post: my post title"
git push
```

GitHub Actions builds and deploys automatically. The post is live in ~1 minute.
