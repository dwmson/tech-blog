---
title: 'Building My Blog with Hugo, Supabase, and GitHub Pages'
date: 2025-02-22
tags: ['Hugo', 'Supabase', 'GitHub Pages', 'CDN', 'Static Site']
---

## Introduction

I wanted to build a personal tech blog that is **fast, easy to manage, and free to host**. I chose **Hugo** as my static site generator, **Supabase Storage** as a CDN for images and other assets, and **GitHub Pages** for hosting.

This post walks through the steps to **set up a Hugo blog, use Supabase for images, and deploy it to GitHub Pages**.

---

## 1. Setting Up Hugo Locally

First, install **Hugo**:

### **Mac (Homebrew):**

```bash
brew install hugo
```

### **Windows (Chocolatey):**

```bash
choco install hugo
```

### **Linux (Ubuntu/Debian):**

```bash
sudo apt install hugo
```

### **Create a New Hugo Site:**

```bash
hugo new site my-tech-blog
cd my-tech-blog
```

### **Install a Theme (Paper Theme Example):**

```bash
git init
git submodule add https://github.com/nanxiaobei/hugo-paper themes/hugo-paper
```

Edit `config.toml` to use the theme:

```toml
theme = "hugo-paper"
title = "My Tech Blog"
baseURL = "http://localhost:1313/"
```

Run the server locally:

```bash
hugo server
```

Now, visit **http://localhost:1313/** to see your blog! 🎉

---

## 2. Using Supabase as a CDN for Images

Since Hugo generates static files, we need a way to host images and assets. **Supabase Storage** provides a CDN, making it easy to store and serve images.

### **Steps to Upload Images to Supabase:**

1. **Sign up** at [Supabase](https://supabase.io/) and create a project.
2. Go to **Storage** → Create a **bucket** (`blog-images`).
3. Upload an image (e.g., `pi-setup.jpg`).
4. Click the image → Copy the **public URL**.

### **Embed Images in a Hugo Post:**

```markdown
![My Raspberry Pi Setup](https://xyz.supabase.co/storage/v1/object/public/blog-images/pi-setup.jpg)
```

This makes images load **fast** without increasing your site's size. 🚀

---

## 3. Deploying Hugo Blog to GitHub Pages

Now that our blog is working locally, let’s **deploy it to GitHub Pages**.

### **Step 1: Create a GitHub Repository**

Go to GitHub and create a new repository (e.g., `my-blog`).

### **Step 2: Push Your Hugo Site to GitHub**

```bash
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/<your-username>/my-blog.git
git push -u origin main
```

### **Step 3: Enable GitHub Pages**

1. Go to **Settings** → **Pages**.
2. Under **Source**, select `Deploy from a branch`.
3. Choose `main` branch and click **Save**.
4. Your blog will be live at:
   ```
   https://<your-github-username>.github.io/my-blog/
   ```

🎉 **Your Hugo blog is now hosted for free on GitHub Pages!**

---

## 4. Automating Deployment (GitHub Actions - Optional)

To **automate Hugo builds and deployments**, set up **GitHub Actions**:

1. Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy Hugo Site
on:
  push:
    branches:
      - main
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
      - run: hugo --minify
      - uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

Now, every time you **push changes to GitHub**, it will rebuild and deploy automatically. 🚀

---

## Conclusion

This guide walked through **setting up a Hugo blog, using Supabase for images, and deploying on GitHub Pages**. Now, I can focus on writing without worrying about hosting costs or performance issues.

💡 **Next Steps:**

- **Customize the blog theme** (modify colors, layouts, fonts).
- **Set up a custom domain** instead of `github.io`.
- **Add a "Projects" page** showcasing GitHub repositories.

Hope this helps others looking to build a tech blog! 🚀

---

Got questions? Let me know in the comments or [reach out on GitHub](https://github.com/your-username). Happy blogging! 😊
