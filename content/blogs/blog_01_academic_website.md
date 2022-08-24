# How to ceate your website using Hugo & Github Pages


**by Mirza Waleed (24-08-2022)**

In this post, I will share how I made [My Portfolio/Bloging Website](waleedgeo.github.io/) using [Github Pages](https://pages.github.com/) and [Hugo](https://gohugo.io/).

Originally, i get inspired from  [this twitter thread](https://mobile.twitter.com/neubadah/status/1558502846265442304) and started preparing [my website](waleedgeo.github.io) from scratch.

For better understanding of whole process install following:

- Install [VS Code](https://code.visualstudio.com/)
- Installl [Hugo](https://gohugo.io/getting-started/installing/) 
- Create a [Github](https://github.com/) account

Install github extension in VS code and login to your github

![github](https://imgur.com/wvNn0QI.png)

Install Hugo by following [this guide ](https://gohugo.io/getting-started/quick-start/)

Then check if Hugo is installed by

```
hugo version
```

If hugo is installed, it will give you something like this

![hugo version](https://imgur.com/Xymc5S0.png)

Then start following this sequence
## Hugo New Site
Open terminal and create a new hugo site using  (<> indicades changes by user)

```
hugo new site <name> -f "yaml"
```

cd to that folder, then add below commands to git init and remote 

```
cd <name>
git init
git add .
git commit -m "initial commit"
```

# Choose your theme

Choose themes from this [website](https://themes.gohugo.io/)

![hugo theme](https://imgur.com/dDJR4Jm.png)

To choose theme, simply go to its download location (github repo) and copy its repo url

The next part is to add a theme inside hugo site foler. Note: it is best to first fork that repo to yours github, then use your forked git repo afterwords (in case you want to customize theme yourself later)

Also change the name of theme to that theme name (i.e., PaperMod etc)

Use below code (with your forked theme repo URL) to download & rename theme

```
git submodule add <forked git repo address OR hugo themes> themes/<name of theme>
```

Now, make any changes you want to do with your yaml config, content, and static/images
after that follow this code to upload materials to github repo

## How to modify?

Yaml or Yml contains main information of your theme. See this [link](https://gohugo.io/getting-started/configuration/) to get an idea of Yaml config working.

After config modiification, create new content (in the form of MarkDown (.md file)). Inside content folder create folder (main root) and then add md files in them. Each md file will be your each post published.

Additional tip: If you just want to include single page (e.g. in my website [About](https://waleedgeo.github.io/about) or [Publications](https://waleedgeo.github.io/publications) just add one md file with name _index.md_ and write anything in MarkDown Format in it.

This is also important for future posts. Whenever you want to add a blog, simply use VS code to include a new file in respective folder and start writing :)

After you have finished writing, follow below commands to commit changes

```
git add .
git commit -m "upload"
git push -u origin main
git status

```

Important step
Make a new repo using this "your github name.github.io" (i.e., waleedgeo.github.io, in which waleedgeo is my github username)

Don't add anythig in it, just create an empty repo on github then follow this code

```
git remote add origin <new repo url>
git push -u origin main
git status

```
---
After you successfully uploaded your content its time to add gh pages files for workflow automation. This helps whenever you add something in your repo, it will be automatically updated in your website.

For that do following

- Create a new folder _.github_ inside your website folder
- Create a new folder _workflows_ inside your _.github_ folder
- Create a new file there with name _gh-pages.yml_
- Copy below code into your _gh-pages.yml_ file ([source](https://gohugo.io/hosting-and-deployment/hosting-on-github/))

```
name: github pages on: push: branches: - main # Set a branch to deploy pull_request: jobs: deploy: runs-on: ubuntu-20.04 steps: - uses: actions/checkout@v2 with: submodules: true # Fetch Hugo themes (true OR recursive) fetch-depth: 0 # Fetch all history for .GitInfo and .Lastmod - name: Setup Hugo uses: peaceiris/actions-hugo@v2 with: hugo-version: 'latest' # extended: true - name: Build run: hugo --minify - name: Deploy uses: peaceiris/actions-gh-pages@v3 if: github.ref == 'refs/heads/main' with: github_token: ${{ secrets.GITHUB_TOKEN }} publish_dir: ./public

```

 Now  again upload the contents to github repo (either by using VS code github extension or below code in terminal)

```
git add
git commit -m "upload gh-pages"
git push
```

Once you have done this, go to your repo url address, select settings, and navigate to pages panel.

In that, change branch from main to gh-pages like below

![gh-pages](https://imgur.com/ogQFFZ0.png)

After that go to repo then actions and wait 2-5 minutes till your github page is deployed

![github actions](https://imgur.com/wzBfaTD.png)

When deployed, go to this url _yourusername_.github.io and check if website is working properly.

![Imgur](https://imgur.com/xVBNbqD.png)

In case if you have any confusion, see below tutorials (which honestly I used to learn all this).

Main tutorial:

[![Y1](https://imgur.com/VL0IiUy.png)](https://www.youtube.com/watch?v=psyz4UPnGAA")
Other resources

- https://www.youtube.com/watch?v=jUPW2unCJEE
- https://www.youtube.com/watch?v=mEZ1Hj5yQ-8


---
If you still have questions, feel free to reach me through my [mail](mailto:waleedgeo@outlook.com) or [LinkedIn](https://www.linkedin.com/in/waleedgeo/).

---