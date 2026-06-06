# Pushing Project ELLE to GitHub: Step-by-Step Guide

Follow these steps carefully to ensure a clean, error-free push of your project to GitHub. This will prepare your project for Vercel and Render/Railway deployments.

> [!CAUTION]
> Before you begin, make sure you do NOT have any `.env` files hardcoded or manually added to your Git track. They contain sensitive credentials. Our `.gitignore` is already set up to prevent this, but double check!

## Step 1: Initialize Git in your Project
First, let's make sure your project is a Git repository and properly staged. Open your VS Code terminal (or standard terminal) in your project root (`c:\Users\megha\Desktop\Projects\ELLE`) and run:

```bash
# 1. Initialize a new git repository (if it isn't one already)
git init

# 2. Add all your project files to Git 
# (The .gitignore file we set up will automatically exclude the heavy node_modules, .venvs, and sensitive files)
git add .

# 3. Commit your files with a clean message
git commit -m "Initial commit: ELLE project base structure"

# 4. Ensure your main branch is called 'main'
git branch -M main
```

## Step 2: Create a New Repo on GitHub
1. Go to [GitHub](https://github.com/) and log in.
2. In the top right corner, click the **+ (Plus)** dropdown icon and select **New repository**.
3. Name your repository (e.g., `elle-microplastic-detector`).
4. **Important**: Leave "Add a README file", "Add .gitignore", and "Choose a license" **UNCHECKED**. (We already have these locally).
5. Click **Create repository**.

## Step 3: Link Local Folder to GitHub
GitHub will show you a page with instructions. Look for the section titled:
_"…or push an existing repository from the command line"_

Copy those commands or run the following in your local terminal:

```bash
# 1. Link your local project to your new GitHub remote 
# (REPLACE 'YOUR_USERNAME' and 'YOUR_REPO_NAME' with the actual ones)
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git

# 2. Push your code to GitHub
git push -u origin main
```

> [!TIP]
> If you get authentication prompts during the `git push`, follow the on-screen instructions to authenticate GitHub with your browser.

## Step 4: Verify the Push
1. Refresh your GitHub repository page.
2. You should now see your project files (`backend/`, `frontend/`, `README.md`, etc.).
3. **Double-Check:** Ensure that `node_modules/`, `backend/.venv/`, and frontend/backend `.env` files are **NOT** visible in the GitHub web interface.

> [!NOTE]
> Once you have successfully pushed your files, let me know! The next step will be to connect this GitHub repository to Vercel (for the frontend website) and Render/Railway (for the Python backend server).
