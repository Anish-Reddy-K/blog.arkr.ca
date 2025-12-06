# Hugo + PaperMod Speedrun Guide 🚀

## ✅ About Deleting Empty Folders

**You're totally fine!** Hugo only uses folders that actually contain files. The folders you deleted:

- **`data/`** - Only needed for data-driven content (JSON/YAML data files)
- **`i18n/`** - Only needed for custom translations (PaperMod already has translations in `themes/PaperMod/i18n/`)
- **`layouts/`** - Only needed when you want to override theme templates (create when needed)

Hugo will recreate these automatically if you add files to them, or you can create them manually when needed.

---

## 🏗️ Hugo Architecture (The Basics)

### Directory Structure
```
blog.arkr.ca/
├── content/          # Your blog posts (markdown files)
├── static/           # Static files (images, CSS, JS) - copied as-is to public/
├── themes/           # Theme files (PaperMod)
├── public/           # Generated HTML (don't edit manually!)
├── hugo.yaml         # Main config file
└── archetypes/       # Templates for new posts
```

### How Hugo Works
1. **Content** (`content/`) - Your markdown files
2. **Config** (`hugo.yaml`) - Site settings
3. **Theme** (`themes/PaperMod/`) - Templates and styling
4. **Build** - Hugo generates `public/` folder with static HTML

---

## 🎨 PaperMod Customization Levels

### Level 1: Configuration Only (Easiest)
**File:** `hugo.yaml`

All customization through config params. No code changes needed!

**Key Sections:**
- `params.title`, `params.description` - Site metadata
- `params.homeInfoParams` - Homepage content
- `params.socialIcons` - Social links
- `params.profileMode` - Profile page mode
- `menu.main` - Navigation menu

### Level 2: Override Templates (Medium)
**Location:** Create `layouts/` folder in root

Hugo's lookup order:
1. `layouts/` (your overrides) ← **Highest priority**
2. `themes/PaperMod/layouts/` (theme defaults)

**Common overrides:**
- `layouts/_default/baseof.html` - Base template
- `layouts/partials/header.html` - Header
- `layouts/partials/footer.html` - Footer
- `layouts/_default/single.html` - Post page
- `layouts/_default/list.html` - List pages

### Level 3: Custom CSS/JS (Advanced)
**Location:** `static/` folder or `assets/` folder

- `static/css/custom.css` - Custom styles
- Reference in `hugo.yaml` via `params.assets` or override `head.html`

---

## 🔧 Common Customizations

### 1. Customize Homepage Content
**File:** `hugo.yaml`

```yaml
params:
  homeInfoParams:
    Title: "Hi there 👋"
    Content: "Welcome to my blog about tech, life, and everything in between!"
```

### 2. Add Custom CSS
**Option A:** Add to `static/css/custom.css`, then override `head.html`:
```html
<!-- layouts/partials/extend_head.html -->
<link rel="stylesheet" href="{{ "css/custom.css" | absURL }}">
```

**Option B:** Use Hugo's asset pipeline (better for minification):
1. Create `assets/css/custom.css`
2. Override `head.html` to include it

### 3. Override Theme Templates
**Example:** Customize footer

1. Copy from theme:
   ```bash
   cp themes/PaperMod/layouts/partials/footer.html layouts/partials/footer.html
   ```
2. Edit `layouts/partials/footer.html` to your liking

### 4. Custom Post Template
Create `layouts/_default/single.html` to customize how posts render.

### 5. Add Custom Shortcodes
Create `layouts/shortcodes/mycode.html`:
```html
<div class="custom-box">
  {{ .Inner }}
</div>
```

Use in markdown: `{{< mycode >}}Content{{< /mycode >}}`

---

## 📝 PaperMod-Specific Features

### Profile Mode
Enable a profile-style homepage:
```yaml
params:
  profileMode:
    enabled: true
    title: "Your Name"
    subtitle: "Your subtitle"
    imageUrl: "/images/profile.jpg"
    buttons:
      - name: Posts
        url: posts
      - name: Tags
        url: tags
```

### Reading Time & Word Count
Already enabled in your config:
- `ShowReadingTime: true`
- `ShowWordCount: true`

### Code Highlighting
You're using Chroma (Hugo's built-in highlighter):
```yaml
pygmentsUseClasses: true
markup:
  highlight:
    noClasses: false
```

### Search
PaperMod includes fast search via Fuse.js. Configure in:
```yaml
params:
  fuseOpts:
    threshold: 0.4
    keys: ["title", "permalink", "summary", "content"]
```

---

## 🎯 Quick Customization Checklist

- [ ] Update `params.title` and `params.description` in `hugo.yaml`
- [ ] Add your social icons in `params.socialIcons`
- [ ] Customize `params.homeInfoParams` for homepage
- [ ] Update `menu.main` for navigation
- [ ] Add favicon in `static/` and reference in `params.assets`
- [ ] Customize colors (if needed) via CSS override
- [ ] Add custom logo/branding

---

## 🚀 Pro Tips

1. **Don't edit `themes/PaperMod/` directly** - Updates will overwrite changes
2. **Use `layouts/` for overrides** - This is the Hugo way
3. **Test locally:** `hugo server` (runs on http://localhost:1313)
4. **Build:** `hugo` (generates `public/` folder)
5. **Drafts:** Set `draft: true` in frontmatter to hide posts
6. **Future posts:** Set future date, use `hugo server -F` to preview

---

## 📚 Resources

- **Hugo Docs:** https://gohugo.io/documentation/
- **PaperMod Docs:** https://github.com/adityatelange/hugo-PaperMod/wiki
- **PaperMod Examples:** https://github.com/adityatelange/hugo-PaperMod/wiki/Examples

---

## 🔍 Your Current Setup

Based on your `hugo.yaml`:
- ✅ PaperMod theme configured
- ✅ Basic params set up
- ✅ Menu configured (categories, tags)
- ✅ Reading time enabled
- ⚠️ Update `params.title` from "ExampleSite" to your actual title
- ⚠️ Update `params.description` from placeholder
- ⚠️ Update social icons URLs
- ⚠️ Consider enabling profile mode or customizing homeInfoParams

---

## 🛠️ Next Steps

1. **Customize your config** - Update all the "ExampleSite" placeholders
2. **Add custom CSS** (if needed) - Create `static/css/custom.css`
3. **Override templates** (if needed) - Create `layouts/` folder
4. **Add favicon** - Put in `static/` and reference in config
5. **Test locally** - `hugo server` and preview changes
