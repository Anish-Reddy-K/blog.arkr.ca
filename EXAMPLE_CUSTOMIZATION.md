# Practical Customization Example 🎨

This guide shows you **exactly** how to customize PaperMod step-by-step.

---

## Example: Adding Custom CSS

### Step 1: Create Custom CSS File

```bash
mkdir -p static/css
```

Create `static/css/custom.css`:
```css
/* Custom styles for your blog */

/* Example: Change link colors */
.post-content a {
    color: #3b82f6;
    text-decoration: underline;
}

.post-content a:hover {
    color: #2563eb;
}

/* Example: Custom code block styling */
.post-content pre {
    border-radius: 8px;
    padding: 1rem;
}

/* Example: Custom heading styles */
.post-content h2 {
    border-bottom: 2px solid #e5e7eb;
    padding-bottom: 0.5rem;
    margin-top: 2rem;
}
```

### Step 2: Include CSS in Your Site

**Option A: Override extend_head.html (Recommended)**

```bash
mkdir -p layouts/partials
cp themes/PaperMod/layouts/partials/extend_head.html layouts/partials/extend_head.html
```

Edit `layouts/partials/extend_head.html`:
```html
<!-- Add your custom CSS -->
<link rel="stylesheet" href="{{ "css/custom.css" | absURL }}">
```

**Option B: Override head.html (More control)**

```bash
mkdir -p layouts/partials
cp themes/PaperMod/layouts/partials/head.html layouts/partials/head.html
```

Then add your CSS link in the `<head>` section.

### Step 3: Test

```bash
hugo server
```

Visit http://localhost:1313 and check if your styles apply!

---

## Example: Customizing Homepage

### Step 1: Update Config

Edit `hugo.yaml`:
```yaml
params:
  homeInfoParams:
    Title: "Welcome to My Blog 🚀"
    Content: |
      This is my personal blog where I write about:
      - Technology
      - Life experiences
      - Random thoughts
      
      Thanks for visiting!
```

### Step 2: Test

```bash
hugo server
```

The homepage will show your custom content!

---

## Example: Overriding Footer

### Step 1: Copy Footer Template

```bash
mkdir -p layouts/partials
cp themes/PaperMod/layouts/partials/footer.html layouts/partials/footer.html
```

### Step 2: Edit Footer

Open `layouts/partials/footer.html` and customize:
```html
<footer class="footer">
    <span>&copy; {{ now.Year }} <a href="{{ "" | absURL }}">{{ site.Title }}</a></span>
    <span>
        Powered by <a href="https://gohugo.io/">Hugo</a> & 
        <a href="https://github.com/adityatelange/hugo-PaperMod">PaperMod</a>
    </span>
    <!-- Add your custom footer content here -->
    <span>Made with ❤️ by Anish</span>
</footer>
```

### Step 3: Test

```bash
hugo server
```

---

## Example: Custom Post Template

### Step 1: Copy Single Template

```bash
mkdir -p layouts/_default
cp themes/PaperMod/layouts/_default/single.html layouts/_default/single.html
```

### Step 2: Customize

Edit `layouts/_default/single.html` to add custom elements:
- Add custom post header
- Change post metadata display
- Add custom post footer
- Modify post content wrapper

### Step 3: Test

```bash
hugo server
```

Visit any post page to see changes!

---

## Example: Adding Custom Shortcode

### Step 1: Create Shortcode

```bash
mkdir -p layouts/shortcodes
```

Create `layouts/shortcodes/alert.html`:
```html
<div class="alert alert-{{ .Get "type" }}" role="alert">
    <strong>{{ .Get "title" }}</strong>
    {{ .Inner }}
</div>
```

### Step 2: Add CSS for Alert

Add to `static/css/custom.css`:
```css
.alert {
    padding: 1rem;
    border-radius: 4px;
    margin: 1rem 0;
}

.alert-info {
    background-color: #dbeafe;
    border-left: 4px solid #3b82f6;
}

.alert-warning {
    background-color: #fef3c7;
    border-left: 4px solid #f59e0b;
}
```

### Step 3: Use in Posts

In your markdown:
```markdown
{{< alert type="info" title="Note" >}}
This is an informational alert!
{{< /alert >}}

{{< alert type="warning" title="Warning" >}}
This is a warning!
{{< /alert >}}
```

---

## Example: Custom Menu Item

### Edit hugo.yaml

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
    - identifier: about
      name: About
      url: /about/
      weight: 30
    - identifier: categories
      name: Categories
      url: /categories/
      weight: 40
    - identifier: tags
      name: Tags
      url: /tags/
      weight: 50
```

Then create `content/about.md`:
```markdown
---
title: "About"
date: 2025-12-02
draft: false
---

This is the about page!
```

---

## 🎯 Quick Test Checklist

After any customization:

1. ✅ Run `hugo server` locally
2. ✅ Check homepage looks correct
3. ✅ Check post pages render properly
4. ✅ Check navigation menu works
5. ✅ Check mobile view (resize browser)
6. ✅ Check dark/light mode toggle
7. ✅ Build production: `hugo` (check for errors)
8. ✅ Verify `public/` folder generated correctly

---

## 💡 Pro Tips

1. **Start small** - Make one change at a time
2. **Test locally** - Always use `hugo server` before deploying
3. **Keep backups** - Git commit before major changes
4. **Check theme updates** - PaperMod gets updates, test after pulling
5. **Use browser dev tools** - Inspect elements to understand structure
6. **Read theme source** - Look at `themes/PaperMod/layouts/` to understand structure

---

## 🐛 Troubleshooting

### Styles not applying?
- Check file path in `extend_head.html`
- Clear browser cache
- Check Hugo output for errors
- Verify CSS file exists in `static/css/`

### Template not overriding?
- Check file path matches theme structure
- Verify file is in `layouts/` not `themes/`
- Check Hugo output for template warnings

### Changes not showing?
- Restart `hugo server`
- Delete `.hugo_build.lock`
- Clear browser cache
- Check you're editing the right file

---

## 📚 Next Steps

1. Try the CSS customization example above
2. Customize your homepage content
3. Update your config with real info
4. Create custom shortcodes for common content
5. Override templates as needed

Remember: **Start simple, test often, iterate!** 🚀
