---
title: "Installing IBM Plex fonts on macOS"
layout: post
date: 2020-04-05 08:12
image: 
headerImage: false
tag:
- macOS
- fonts
star: false
category: blog
author: prashant
hidden: false
description: How to install IBM Plex fonts on your mac
---

This post is guide to install [IBM Plex](https://github.com/IBM/plex) fonts on your mac.

1. Download the most recent version of TrueType fonts from [IBM Plex github release page](https://github.com/IBM/plex/releases) named `TrueType.zip`.

2. Open the terminal of your choice and go to the directory where `TrueType.zip` file is downloaded.

   ```bash
   cd ~/Downloads
   ```

3. Unzip the file:

   ```bash
   unzip TrueType.zip
   ```

4. If you want to install the fonts for system wide use, you have to copy all the ttf files to `/Library/Fonts/` directory or if you want to install the fonts only for the use of current user, you have to copy all the ttf files to `~/Library/Fonts/` directory.

   For system wide use:

   ```bash
   cp TrueType/*/*.ttf /Library/Fonts/
   ```

   Only for current user:

   ```bash
   cp TrueType/*/*.ttf ~/Library/Fonts/
   ```

That's it!!! IBM Plex fonts are installed on your mac. You can follow similar procedure to install any `.ttf` or `.otf` font file on mac.
