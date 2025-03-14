+++
title = 'Install Static Website With Hugo and Deploy to Cloudflare'
date = 2025-03-14T13:58:26-07:00
draft = true
+++
I understand, let's make sure it's formatted correctly for Markdown. Here is the guide in proper Markdown format:

# Creating a Static Website with Hugo and Deploying to Cloudflare

## Prerequisites
- Install Hugo
- Install Git
- Create a Cloudflare account

## Step 1: Install Hugo
### Windows
1. Download the latest Hugo release from the Hugo Releases page.
2. Extract the downloaded file.
3. Move the `hugo.exe` file to a directory included in your system's `PATH`.

### macOS
1. Install Homebrew if you haven't already:
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
Install Hugo using Homebrew:
brew install hugo
Linux
Download the latest Hugo release from the Hugo Releases page.
Extract the downloaded file.
Move the hugo binary to /usr/local/bin:
sudo mv hugo /usr/local/bin/
Step 2: Install Git
Windows
Download the Git installer from the Git for Windows page.
Run the installer and follow the setup instructions.
macOS
Install Git using Homebrew:
brew install git
Linux
Install Git using your package manager. For example, on Debian-based systems:
sudo apt install git
Step 3: Create a Cloudflare Account
Go to the Cloudflare Sign-Up page.
Enter your email and password.
Click Create Account.
Verify your email address by clicking the link sent to your email.
Step 4: Create a New Hugo Site
Open your terminal.
Run the following command to create a new Hugo site:
hugo new site my-website
Navigate to your new site directory:
cd my-website
Step 5: Add a Theme
Choose a theme from the Hugo Themes website.
Add the theme as a Git submodule:
git init
git submodule add https://github.com/<theme-repo> themes/<theme-name>
Edit the config.toml file to use the new theme:
theme = "<theme-name>"
Step 6: Add Content
Create a new post:
hugo new posts/my-first-post.md
Edit the newly created file in content/posts/my-first-post.md and add your content.
Step 7: Build the Site
Generate the static files:
hugo
The generated files will be in the public directory.
Step 8: Push to GitHub
Initialize a new Git repository:
git init
Add your files and commit:
git add .
git commit -m "Initial commit"
Add your GitHub repository as a remote using SSH:
git remote add origin git@github.com:<your-username>/<your-repo>.git
Push your changes:
git push -u origin main
Step 9: Deploy to Cloudflare Pages
Log in to your Cloudflare account.
Go to Workers & Pages > Create application > Pages > Connect to Git.
Select your GitHub repository.
Configure the build settings:
Production branch: main
Build command: hugo
Build output directory: public
Click Save and Deploy.
Your site will be deployed to a unique subdomain on *.pages.dev. Cloudflare Pages will automatically rebuild and deploy your site on new commits.

Conclusion
You have successfully created a static website using Hugo and deployed it to Cloudflare Pages. Enjoy your new site!
