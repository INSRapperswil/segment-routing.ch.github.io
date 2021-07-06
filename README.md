# segment-routing-ch-source
This repository contains the source code of the website https://www.segment-routing.ch.
This website has been built with [Hugo](https://gohugo.io/) and is deployed as a GitHub Pages site.

## GitHub Pages
The website is hosted by GitHub Pages in this repository:  
https://github.com/INSRapperswil/segment-routing-ch.github.io
This repository has been added as a submodule to the folder `segment-routing/public` of this project.

## Theme
The theme of the website is managed by this repository:  
https://github.com/INSRapperswil/segment-routing-ch-theme
This repository has been added as a submodule to the folder `segment-routing/themes/segment-routing-ch-theme` of this project.

## DevOps
Making changes to the website's content or styling is all done through this repository. The repositories `segment-routing-ch.github.io` and `segment-routing-ch-theme` are both added to this project as submodules and do not have to be pulled seperately.
The image below illustrates the DevOps of this project.

![DevOps Diagram](https://raw.githubusercontent.com/INSRapperswil/segment-routing-ch-source/master/images/dev-ops-diagram.png)


## Setting Up the Development Environment
Follow these steps to setup the development environment. This is required to make changes to the website's content and styling.

### Install Hugo
Install `hugo` on your computer by following the [official guide](https://gohugo.io/getting-started/installing/).
If you are on Linux you can simply type:
```bash
sudo apt update
sudo apt install hugo
```

### Clone & Initialize the Repository
First, clone this repository:
```bash
git clone git@github.com:INSRapperswil/segment-routing-ch-source.git
```
Then initialize and update the submodules by running the `init-dev-env.sh` script:
```bash
cd segment-routing-ch-source
./init-dev-env.sh
```

## Making Changes to the Website
Making changes to the website requires the development environment to be setup (see chapter [Setting Up the Development Environment](#setting-up-the-development-environment)).

### Important Folders
For most basic operations (such as adding and editing articles or projects) only two directories are important:  
`segment-routing/content/english` and `segment-routing/static/images`



- `segment-routing/content/english` contains all content related Markdown-files. They are organized in folders such as `articles` and `projects`.

		segment-routing/content/english/
		├── _index.md
		├── articles
		│   ├── _index.md
		│   ├── article-1.md
		│   ├── article-2.md
		│   └── article-3.md
		└── projects
		    ├── _index.md
		    ├── project-1.md
		    ├── project-2.md
		    └── project-3.md
- `segment-routing/static/images` contains the images for the articles and projects. They are organized in folders that match the Markdown-Filename.
		
		segment-routing/static/images	
		├── articles
		│   ├── article-1
		│   │   ├── article-1-1.jpg
		│   │   └── article-1-2.jpg
		│   └── article-2
		│       └── some-image.jpg
		└──  projects
		    ├── project-1
		    │   ├── project-1-1.png
		    │   ├── project-1-2.png
		    │   └── project-1-3.png
		    ├── project-2
		    │   └── project-overview.png
		    └── project-3
		        └──  a-really-beautiful-image.png

### Creating a New Article or Project
Run one of these commands in the root directory of the project ...
- to create a new <ins>new article</ins>:
	```bash
	hugo new --kind article segment-routing/content/english/articles/<file-name>.md
	```
- to create a new <ins>new project</ins>:
	```bash
	hugo new --kind project segment-routing/content/english/projects/<file-name>.md
	```
Make sure to replace `<file-name>` with a new and unique name.

Now you can edit the Markdown-File and add your content. You can store your images according to the folder structure described in the chapter [Important Folders](#important-folders).

#### Front Matter
At the top of the file you will see code that is enveloped by `---` that looks something like this:
```yaml
---
title: "Article 1"
date: 2000-04-18T10:07:21+06:00
image: "path/to/image"
sliderImages:
  - "path/to/first-image"
  - "path/to/second-image"
  - "path/to/third-image"
type: "featured"
onHomepage: true
description: "This is meta description"
draft: false
buttonLabel: "Read more"
---
```
This is called front matter, and is simply the files metadata written in `YAML`.  You can manually update this values according to your needs.
- `title`
	- The title of your article or project.
- `date`
	- Typically the creation date of your article or project. 
	- This date is also used to sort articles and projects chronologically on the website.
- `image`
	- The path to the main image, which is shown in the overview pages. Of course you can add additional images in the content of the file.
- `sliderImages`
	- Only relevant for projects.
	- The paths to the individual images used for the sliders in the overview page https://www.segment-routing.ch/projects
- `type`
	- Only relevant for articles.
	- This field can be set to either `"featured"` or `"regular"`.
	- If it is set to `"featured"` it will be shown as the featured article on https://www.segment-routing.ch/articles
	- Only one article should be set to `"featured"`, all others should be regular. Even if multiple articles are set to `"featured"`, only one is shown as featured.
- `onHomepage`
	- Only relevant for articles.
	- If set to `true`, the article is shown on the homepage. You can show as many articles as you want on the homepage.
- `description`
	- This string is the meta description that is used by search engines to provide users with more information on the website.
![Meta Description](https://raw.githubusercontent.com/INSRapperswil/segment-routing-ch-source/master/images/meta-description.png)
- `draft`
	- If set to `true`, it will only show up during development, but not when the website is deployed. Even if a draft is pushed to the deployment server, it is not accessible through the internet.
- `buttonLabel`
	- The label of the buttons in overview pages. This can be any string, such as `"Read more"` or `"Check it out"`.

### Testing the Website
To see test the website locally before deploying it, `cd` into the website folder and start a local server:
```bash
cd segment-routing
hugo server
```
This will start a webserver on http://localhost:1313

### Deploying the Website
Once you are happy with your changes, you can build and deploy the website. In the root of the project, run this command:
```bash
./build-site.sh
```
 This will compile the code and update the content in the directory `segment-routing/public`.
 If it was able to build without errors, the site is ready to be deployed. Run this command: 
```bash
./deploy-site.sh "Provide a commit message"
```
This will push the content of the directory `segment-routing/public` to the GitHub Pages repository `segment-routing-ch.github.io`.

## Updating the Theme
If you want to make changes to the styling or otherwise update the theme, you can do so by editing the files in `segment-routing/themes/segment-routing-ch-theme`.

Once you have made your changes, you need to remember to commit them to the themes repository. To do that, run this command in the root of the project:
```bash
./commit-theme-changes.sh
```
