+++
date = "2016-01-21T14:10:00+08:00"
title = "article5"
+++

hugoThemes
All Themes Hugo

See a complete listing of all of these themes along with screenshots and demos at themes.gohugo.io.

Every theme in this list will automatically be added to the theme site.

Installing Themes
Installing all themes

If you would like to install all of the available Hugo themes, simply clone the entire repository from within your working directory with this command:

git clone --depth 1 --recursive https://github.com/spf13/hugoThemes.git themes
Installing a single theme

mkdir themes
cd themes
git clone URL_TO_THEME
Adding a theme to the list
Create your theme using hugo new theme THEMENAME;
Test your theme against https://github.com/spf13/HugoBasicExample;
Add a theme.toml file to the root of the theme;
Add a README.md to the root of the theme;
Add /images/screenshot.png and /images/tn.png;
Open up a new Issue with a link to the theme's repository on GitHub.
If your theme doesn't fit into the Hugo Basic Example site, we encourage theme authors to supply a self-contained Hugo site in /exampleSite. NOTE: The folder name here is important, as this folder will be picked up and used by the script that generates the Hugo Theme Site. See Artist theme's exampleSite for a good example. And please make the site's content as neutral as possible.

Each theme needs:

to be added to the hugoThemes repo;
the right fields in theme.toml;
the right images;
a good README.
theme.toml

The following fields are required:

name = "Hyde"
license = "MIT"
licenselink = "https://github.com/spf13/hyde/blob/master/LICENSE.md"
description = "An elegant open source and mobile first theme"
homepage = "http://siteforthistheme.com/"
tags = ["blog", "company"]
features = ["blog", ]
min_version = 0.13

[author]
    name = "spf13"
    homepage = "http://spf13.com/"

# If porting an existing theme
[original]
    author = "mdo"
    homepage = "http://hyde.getpoole.com/"
    repo = "https://www.github.com/mdo/hyde"
Notes:

This is different from the file created by hugo new theme in the old v0.12. The current Hugo v0.13 does create the same template with the new fields except min_version that was created in 0.14-DEV.

Only theme.toml is accepted, not theme.yaml, not theme.json.

Media

Thumbnail should be 900×600 in pixels
Screenshot should be 1500×1000 in pixels
Media must be located in:
[ThemeDir]/images/screenshot.png
[ThemeDir]/images/tn.png
Additional media may be provided in that same directory.

README

The README file serves double purposes. It is used on GitHub as the content for the main page. It is also used as the content on the detailed theme view page for themes.gohugo.io. It should be in Markdown format and called README.md.