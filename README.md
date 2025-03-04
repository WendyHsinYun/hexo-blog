# HY's BLOG

## Description
This is a personal note website built with Hexo, using the [Icarus theme](https://ppoffice.github.io/hexo-theme-icarus/).

📌 Visit [my blog](https://www.hychang.me)

## Prerequisites

Before you begin, ensure you have the following installed:

1. **Node.js and npm**
   - Hexo requires Node.js version 14 or higher.
   - [Download Node.js](https://nodejs.org/) and verify the installation:
     ```bash
     node -v  # Check Node.js version
     npm -v   # Check npm version
     ```

2. **Git**
   - Used for version control and deployment.
   - [Download Git](https://git-scm.com/downloads) and verify the installation:
     ```bash
     git --version
     ```

## Installation

1. **Install Hexo CLI globally:**
   ```bash
   npm install -g hexo-cli
   ```

2. **Verify Hexo installation:**
   ```bash
   hexo -v
   ```

3. **Clone the repository:**
   ```bash
   git clone https://github.com/WendyHsinYun/hy-blog
   cd hy-blog
   ```

4. **Install dependencies:**
   ```bash
   npm install
   ```

## Install Icarus Theme

### Method 1: Clone the Theme

1. **Clone the Icarus theme:**
   ```bash
   git clone https://github.com/ppoffice/hexo-theme-icarus.git themes/icarus --depth 1
   ```

2. **Set Icarus as the theme:**
   ```bash
   hexo config theme icarus
   ```

### Method 2: Add as Git Submodule

1. **Add Icarus theme as a Git submodule:**
   ```bash
   git submodule add https://github.com/ppoffice/hexo-theme-icarus.git themes/icarus
   ```

2. **Set Icarus as the theme:**
   ```bash
   hexo config theme icarus
   ```

> **Note:** Using Git submodules makes it easier to update the theme in the future. Run `git submodule update --remote` to pull the latest changes.

## Configuration

1. **Update `_config.yml` file**  
   Modify `title`, `description`, `url`, etc., based on your needs.

2. **Configure Icarus theme (`themes/icarus/_config.yml`)**  
   Customize theme colors, navigation, plugins, and more.

## Quick Start

### Create a New Post

```bash
hexo new "My New Post"
```

For more information: [Writing](https://hexo.io/docs/writing.html)

### Run Local Server

```bash
hexo server
```

By default, it runs at [http://localhost:4000](http://localhost:4000).  
For more information: [Server](https://hexo.io/docs/server.html)

### Generate Static Files

```bash
hexo generate
```

For more information: [Generating](https://hexo.io/docs/generating.html)

### Deploy to GitHub Pages

1. Ensure the `deploy` section in `_config.yml` is correctly set:
   ```yml
   deploy:
     type: git
     repo: https://github.com/WendyHsinYun/hy-blog.git
     branch: gh-pages
   ```

2. Run the deploy command:
   ```bash
   hexo deploy
   ```

For more information: [Deployment](https://hexo.io/docs/one-command-deployment.html)

## Common Commands Summary

| Command                                                      | Description                                 |
|--------------------------------------------------------------|---------------------------------------------|
| `hexo new "My New Post"`                                      | Create a new post                          |
| `hexo clean`                                                 | Clear cache                                |
| `hexo generate`                                              | Generate static files                      |
| `hexo server`                                                | Run local server                           |
| `hexo deploy`                                                | Deploy to remote site                      |
| `git submodule update --remote`                               | Update theme if added as submodule         |

## Useful Links

- [Hexo Documentation](https://hexo.io/docs/)
- [Icarus Theme Documentation](https://ppoffice.github.io/hexo-theme-icarus/)
