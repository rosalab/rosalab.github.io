# A Website Template for the ROSA Lab @ CSVT

## Introduction 

This is a statically-generated Jekyll/Liquid/Bootstrap-based website template for academics.
This website is inspired from [Dr. Spencer's](https://github.com/sbryngelson/academic-website-template#hosting) and [Allan lab's](https://www.allanlab.org/) webpage templates. These templates have been modified to meet our requirements.

The documentation for how to use this template has been provided in the remainder of this document.
In short, there are three steps to be noted:

* [Fork](#fork-and-build)
* [Customize](#customization)
* [Host](#hosting)

## Fork and Build

Fork [the current repository]() by clicking the `fork` button in the top-right corner of the Github webpage.
There are two ways you can use to set up the build environment: Natively or via a Docker container. 

* If you want to build the site natively, you will need the following dependencies: 
    * Python (Version greater than 3.7 preferred)
    * Bibble (After installing python, `pip install bibble`)
    * Ruby (also the ruby development tools. It would be `ruby-devel` or `ruby-dev` depending on your system)
    * Jekyll (version 4.1.1 or less required. After installing Ruby, `gem install jekyll -v <version_number>`)
    * Thin (`gem install thin`)
    * Jekyll scholar (`gem install jekyll-scholar`)
* Run `$ bundle exec jekyll serve` in the repository root directory. The site will be hosted locally at `localhost:4000`
* It will automatically re-build the changes to the files once you save them.

* To build via the Docker container, you will need the following dependencies:
   * [Docker](https://docs.docker.com/engine/install/)
   * This [Docker Image](https://hub.docker.com/r/bretfisher/jekyll-serve/). It provides you a readymade container to run your website.
   * In order to build the site, from the website root directory execute `sudo docker run -p 4000:4000 -v $(pwd):/site bretfisher/jekyll-serve`
   * This should run the website at `0.0.0.0:4000`.

There is one important thing to note about Jekyll plugins:
* This webpage uses Jekyll plugins (e.g., Jekyll Scholar) to automatically build the bibliography. 
  Since we are using Github pages, we will need to build the site with `Rakefile` in the root directory of the source branch.
  This can be done by modifying the files as appropriate and then, after pushing your changes, execute `rake publish`.

## Customization

* `_config.yml` is where the basic details of the website is stored. You would mostly not be needed to modify this.
* The YAML database files, located in `_data/*.yml`, contains the details that would need to be added to the site.
  This includes our personal details and news. Again, `awards.yml`,`funders.yml`,`grants.yml`,`pi.yml` would be the least modified. 
* The individual pages located in `_pages/*.md` is where we will be handling details for news, research and teaching.
* The `assets` folder contains the file and folder where we add the publication details and personal/project photos.

Further details are provided below:

### Navbar

The pages listed in the top navbar are located in `_config.yml` file.
The typical options are included/commented for convenience. Follow the similar convention for adding/listing pages.

### Creating or editing pages

All pages are located in the `_pages` directory.
Pages generally load information from YAML databases located as `_data/*.yml`.
Creating new pages can be done by using existing pages as a template.

#### Page header information

All pages require header information.
An example header data for the 'Talks' page is shown below:
```
---
title: "Talks"
layout: gridlay
sitemap: false
permalink: /talks/
---
```
The `layout` variable corresponds to HTML layouts in the `_layouts` directory.
The differences between most layouts is subtle and `gridlay` can generally be used.
The permalink must be unique for each page, and corresponds to the directory that will store the page in the compiled HTML.
Refer to your pages in `_config.yml` via the `title` variable.

#### Markdown

All pages are written in [Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) as `*.md`.
HTML commands and CSS styles can be directly used in markdown files.

#### Publication page and database

As mentioned earlier, the publications and talks are listed via Jekyll Scholar.
The bibliography file `ref.bib` is located in the `cv/` directory.
You can modify this according to your needs.

## Hosting

Once your site has been modified to fit your needs, you can push your changes to the main GitHub repository.
This is currently a work in progress.

## Acknowledgment

I would like to credit [Dr. Spencer Bryngelson](https://github.com/sbryngelson) and [Allen Lab](https://www.allanlab.org/) for creating wonderful templates geared towards academic research groups. This website was adapted from their laboratory webpage templates.

## License

Copyright 2023, ROSA@VTCS and controlled via the MIT license.
You are allowed to copy and mess with the template.