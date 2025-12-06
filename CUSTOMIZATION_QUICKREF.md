# PaperMod Quick Reference 🎯

## 🗂️ Folder Hierarchy (When to Create What)

```
blog.arkr.ca/
├── content/              # ✅ You have this - blog posts
├── static/               # ✅ You have this - images, custom CSS/JS
├── layouts/              # ⚠️ Create when overriding theme templates
├── assets/               # ⚠️ Create for Hugo asset pipeline (CSS/JS processing)
├── data/                 # ⚠️ Create for data-driven content (rarely needed)
├── i18n/                 # ⚠️ Create for custom translations (rarely needed)
└── themes/PaperMod/      # ✅ Don't edit directly!
```

**Rule:** Only create folders when you need them. Empty folders do nothing.

---

## 🎨 Customization Methods (Priority Order)

### Method 1: Config Only (Easiest) ⭐
**File:** `hugo.yaml`
- Change colors, text, settings
- No code knowledge needed
- **Best for:** Most customizations

### Method 2: Override Templates (Medium)
**Location:** `layouts/` folder
- Copy template from `themes/PaperMod/layouts/`
- Edit your copy
- **Best for:** Changing HTML structure

### Method 3: Custom CSS (Advanced)
**Location:** `static/css/custom.css` or `assets/css/custom.css`
- Add custom styles
- Override theme CSS
- **Best for:** Visual tweaks

---

## 🔧 Most Common Customizations

### 1. Update Site Info
```yaml
params:
  title: "Anish Reddy's Blog"  # Change from "ExampleSite"
  description: "Your actual blog description"
  author: "Anish Reddy"  # Change from "Me"
```

### 2. Customize Homepage
```yaml
params:
  homeInfoParams:
    Title: "Hi there 👋"
    Content: "Your welcome message here"
```

### 3. Add Social Links
```yaml
params:
  socialIcons:
    - name: github
      url: "https://github.com/yourusername"
    - name: x
      url: "https://x.com/yourusername"
    # Remove ones you don't use
```

### 4. Customize Menu
```yaml
menu:
  main:
    - identifier: home
      name: Home
      url: /
      weight: 10
    - identifier: posts
      name: Posts
      url: /posts/
      weight: 20
    # Remove "example.org" entry
```

### 5. Enable Code Copy Buttons
```yaml
params:
  ShowCodeCopyButtons: true  # Change from false
```

### 6. Show Table of Contents
```yaml
params:
  showtoc: true  # Change from false
  tocopen: true  # Auto-expand TOC
```

---

## 📁 Template Override Examples

### Override Footer
```bash
# Copy theme template
cp themes/PaperMod/layouts/partials/footer.html layouts/partials/footer.html

# Now edit layouts/partials/footer.html
```

### Override Post Template
```bash
# Copy theme template
cp themes/PaperMod/layouts/_default/single.html layouts/_default/single.html

# Now edit layouts/_default/single.html
```

### Add Custom CSS
```bash
# Create custom CSS file
mkdir -p static/css
touch static/css/custom.css

# Then override head.html to include it
cp themes/PaperMod/layouts/partials/extend_head.html layouts/partials/extend_head.html
# Add: <link rel="stylesheet" href="{{ "css/custom.css" | absURL }}">
```

---

## 🎯 Hugo Lookup Order (Important!)

When Hugo looks for templates, it checks in this order:

1. **`layouts/`** ← Your overrides (highest priority)
2. **`themes/PaperMod/layouts/`** ← Theme defaults

**This means:** Files in `layouts/` override theme files with the same path.

---

## 🚀 Common Commands

```bash
# Start dev server (with drafts)
hugo server -D

# Start dev server (no drafts)
hugo server

# Build site
hugo

# Build with drafts
hugo -D

# Build with future posts
hugo -F
```

---

## 📝 Post Frontmatter Cheat Sheet

```yaml
---
title: "My Post Title"
date: 2025-12-02
draft: false  # true = hidden, false = published
tags:
  - tag1
  - tag2
categories:
  - category1
description: "Post summary for listings"
cover:
  image: "/images/cover.jpg"
  alt: "Cover image alt text"
---
```

---

## 🎨 PaperMod-Specific Features

### Profile Mode (Alternative Homepage)
```yaml
params:
  profileMode:
    enabled: true
    title: "Your Name"
    subtitle: "Your subtitle"
    imageUrl: "/images/profile.jpg"
```

### Reading Time
Already enabled! Shows estimated reading time on posts.

### Search
Already configured! Press `/` or click search icon.

### Dark/Light Mode
Already enabled! Users can toggle via button.

---

## ⚠️ Common Mistakes

1. ❌ **Editing `themes/PaperMod/` directly** - Updates will overwrite
2. ✅ **Use `layouts/` for overrides** - This is the Hugo way
3. ❌ **Putting images in wrong place** - Use `static/images/`
4. ✅ **Reference images as `/images/filename.png`** in markdown
5. ❌ **Forgetting to rebuild** - Run `hugo` after config changes

---

## 🔍 Debugging Tips

1. **Check Hugo output:** Look for warnings/errors when running `hugo server`
2. **Clear cache:** Delete `.hugo_build.lock` if things seem stuck
3. **Check file paths:** Use relative paths from `static/` or absolute URLs
4. **Validate YAML:** Use online YAML validator if config breaks
5. **Check theme version:** Make sure PaperMod is up to date

---

## 📚 Key Files to Know

- **`hugo.yaml`** - Main config (edit this!)
- **`content/posts/*.md`** - Your blog posts
- **`static/`** - Static assets (images, CSS, JS)
- **`layouts/`** - Template overrides (create when needed)
- **`themes/PaperMod/`** - Theme files (don't edit!)

---

## 🎓 Understanding Hugo Concepts

### Content Organization
- **Sections:** Folders in `content/` become sections (e.g., `content/posts/` = `/posts/`)
- **Frontmatter:** YAML at top of markdown files (metadata)
- **Taxonomies:** Tags and categories (already configured)

### Template System
- **Base template:** `baseof.html` - Wraps everything
- **Single:** `single.html` - Individual post/page
- **List:** `list.html` - List of posts
- **Partials:** Reusable components (header, footer, etc.)

### Asset Pipeline
- **Static:** Files copied as-is (images, fonts)
- **Assets:** Files processed by Hugo (CSS, JS minification)

---

## ✅ Your Current Status

Based on your setup:
- ✅ Basic config working
- ✅ PaperMod theme active
- ✅ Posts rendering
- ⚠️ Update placeholders in `hugo.yaml`
- ⚠️ Remove example menu item
- ⚠️ Update social icon URLs
- 💡 Consider enabling code copy buttons
- 💡 Consider showing table of contents
