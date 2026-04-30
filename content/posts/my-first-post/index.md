
---
date: '2026-04-30T19:13:16+07:00'
draft: false
title: 'How I Built This Static Site'
tags: ["hugo", "webdev"]
summary: "A deep dive into why i chose hugo over WordPress or others for my portofolio"
---
![Hugo Logo](image.png)

Before I jump into the technical dive into the creation of this website, I would like to review some cool informations that you might want to know. But if you want no ~~Buls***~~ just scroll down to the almost buttom section of this blog post. :) 

## Why Hugo?
 Because it's **static** and it's fast, **Really fast...**

## Why Not Wordpress?
Because I don't want to have any **server-side processing at runtime**. While it still lives on a server, its role is strictly to deliver **pre-built files** rather than generate content on the fly.

### How Static "Server-Side" Works?
On a static site, the server acts like a simple file delivery service:

- **No Runtime Logic**: The server does not run scripts (like PHP or Python) or query a database when a user visits a page.
- **Pre-Built Files**: Every pages exists as complete HTML file before anyone even visits.
- **Build-Time Processing**: Any "server-side" work happens **before deployment** during a "build step". it takes your raw code and generate the final static files thar are then uploaded to the server.

#### Difference between Dynamic site & Static site 

- **A Dynamic site is like a (Whiteboard)**: The server "draws" the page from scratch every time someone looks at it.
- **A Static site is like a (Book)**: The page is already "printed." To change the content, you don't edit the live page; you **print a new edition** and swap it out.

### Hugo vs WordPress for blog and porto: **The "No-Nonsense" Breakdown**

If you’re building a blog or portfolio, you want it to be fast, cheap, and impossible to break. Here is why Hugo wins over the "old school" WordPress approach.

#### 1. Insane Loading Speeds
- WordPress: Slow. Every time someone visits, the server has to "build" the page using a database. This creates lag.
-Hugo: Instant. Your pages are already built as simple HTML files. The server just hands them over. There is zero waiting time for your readers.
#### 2. Zero Maintenance Stress
- **WordPress**: Constant headaches. You have to update plugins, themes, and the WordPress core every week. If one update fails, your whole site can crash.
- **Hugo**: Set it and forget it. There are no plugins to break and no database to manage. Once you deploy it, it stays online forever without you touching it.
#### 3. Bulletproof Security
- **WordPress**: A huge target for hackers. Because it has a login page and a database, it’s vulnerable to "brute force" and "SQL injection" attacks.
= **Hugo**: Nothing to hack. Since there is no database or backend code running on the server, there is no "door" for hackers to walk through. It is the most secure way to host a site.
#### 4. Hosting for $0.00
- **WordPress**: Requires "Specialized Hosting" that usually costs $10–$30/month to keep it running smoothly.
- **Hugo**: Can be hosted for free on platforms like GitHub Pages, Netlify, or Vercel. Because static files are lightweight, these companies don't charge you to host them.
#### 5. Better Writing Workflow
- **WordPress**: You have to log into a clunky dashboard and use a "block editor" that can be laggy and frustrating.
- **Hugo**: You write in Markdown (.md). It’s clean, lightweight, and works in any text editor. You own your files locally, so you can write even when you’re offline.

### Technical Dive 
It is very easy to create your first hugo static site, you can visit [Hugo](https://gohugo.io/) and look for [Docs](https://gohugo.io/documentation/) page for the full documentation, then you will find all technical informations for making static website. Anyway I'll cover the **technical fundamentals** for creating a static site.

#### Step 1. Install Hugo

You need the **Extended Version** of Hugo to handle modern CSS features.

- **MacOS**: 
```bash
brew install hugo
```
If you hadn't install Homebrew you can check their website [Homebrew](https://brew.sh/) for technical guide of the installation.

- **Windows**
```powershell
#built-in
winget install Hugo.Hugo.Extended
#with chocolatey
choco install hugo-extended
#or with scoop
scoop install hugo-extended
```
[Scoop](https://scoop.sh/), 
[Choco](https://chocolatey.org/install)

- **Linux**
```bash
sudo apt install hugo
```
#### Step 2: Create the Project
- **Linux & MacOS**
```bash
hugo new site my-first-blog
cd my-first-blog
git init
```
- **Windows**
```powershell
hugo new site my-first-blog
cd my-first-site
git init
```
- `hugo.toml`: The brain of your site. All global settings go here.
- `content/`: Where your Markdown files (the blog posts) live.
- `themes/`: Where the design files live.
- `public/`: This folder doesn't exist yet, but it's where the final "baked" HTML files will go.

#### Step 3: Add the Theme (PaperMod)
I use PaperMod for simple & minimalist theme, perfect for my portofolio.

- **Linux & MacOS**
```bash
git submodule add --depth=1 https://github.com/adityatelange/hugo-paperMod.git themes/PaperMod
echo "theme = 'PaperMod'" >> hugo.toml
```

- **Windows**
```powershell
git submodule add https://github.com/adityatelange/hugo-paperMod.git themes/PaperMod
echo "theme = 'PaperMod'" >> hugo.toml
```
we use `git submodules` so you can easily update the theme later without overwriting your own changes.

#### step 4: Add cool configuartion
open `hugo.toml` in your favourite code editor in this case i use **vscode**

```toml
title = "My Focus Blog"
theme = "PaperMod"

[params]
    env = "production"
    title = "Your Name"
    description = "Thoughts on tech and life."
    ShowReadingTime = true
    ShowShareButtons = true
    defaultTheme = "auto" # This enables the auto Dark/Light mode switch
    
    [params.homeInfoParams]
        Title = "Hi there \U0001F44B"
        Content = "Welcome to my corner of the web. I write about things that matter."
    
    [params.profileMode]
        enabled = false # Set to true if you want a social profile home page
```
#### Step 5: Write Your First Post
```bash
hugo new posts/hello-world.md
```
**Sample**:
```md
---
date: '2026-04-30T19:13:16+07:00'
draft: false
title: 'How I Built This Static Site'
tags: ["hugo", "webdev"]
summary: "A deep dive into why i chose hugo over WordPress or others for my portofolio"
---
```
Open `content/posts/hello-world.md` and write some content. **Important** Change `draft: true` to `draft: false` when you want to see it live.

#### Step 6: See it in Action
Run the local Development server:
```bash
hugo server -D
```
Go to http://localhost:1313.

The server watcher your files. Every time you save a Markdown post, the site "rebuilds" instantly. This is why developers love Hugo it's the fastest SSG in the world.

#### Next: Suggestion & Importance.
Once you have the basics, you can add some cool features such as **Fuzzy Search**, **Shortcodes**, **Image Processing** etc... 

And you also want to learn some basic markdown language such as:

- **Front Matter**
 The stuff between `---` is data about the post hugo uses this to sort your posts by date, add tags and generate the title.

- **Headers**: 
```
"#" H1
"##" H2 
"###" H3
"####" H4
```
- **The syntax text**: 
```
"```python
print("whatever) ```"
``` 
for python, 
```
"```bash 
bash-syntax ```"
```
for bash and etc....

- **Unordered list**:

use **"-"** or **"+"**.

```
- first
- second
- third
```
 
 **or**

```
 + first
 + second
 + third
 ```
**sublists**
```
- first
    - one
    - two
    - three
- second
    - one 
    - two
```

- **Text highlighting & Stressing**
    - `**word**` for __bold__
    - `*word**`  for _italic_ 
    - `***word***` for ***bold & italic***
    - `~~word~~` for ~~strikethrough~~

***for underline and highlight you have to use html***

- **image & link**
```md
#image
![description](image1.png)
#link
[text](https://example.com)
```

#### Final step: Deployment
Static websites are free to host. use **GitHub Pages** or **Netlify**.

- **Netlify**: Just connect your GitHub repo. It will run the **hugo** command every time you "git push" and your site will be updated in seconds.

### Summary: Why this is "Cool"
- **No Database**: Your site can't be hacked via SQL injection.
- **Instant Speed**: Because there is no processing on the server, your pages load in miliseconds.
- **Markdown**: You own your content. it's just text files. if you want to leave Hugo in 10 years, you just take your .md files with you.
- ***Thanks :)***