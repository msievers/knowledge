---
title: WebStorm Text editor
summary:
---

There are a variety of text editors available, but I like WebStorm the best because it groups files into projects, which makes it easy to find all instances of a text string, to do find and replace operations across the project, and more.

If you decide to use WebStorm, here are a few tips on configuring the editor.

## Remove unnecessary plugins

By default, WebStorm comes packaged with a lot more functionality than you probably need. You can lighten the editor by removing some of the plugins. Go to **WebStorm > Preferences > Plugins** and clear the check boxes of plugins you don't need.

## Add the Markdown Support plugin

Since you'll be writing in Markdown, having color coding and other support for Markdown is key. Install the Markdown Support plugin by going to **WebStorm > Preferences > Plugins** and clicking **Install JetBrains Plugin**. Search for **Markdown Support**.

## Learn a few key commands

|Command | Shortcuts |
|-------|--------|
| Shift + Shift | Allows you to find a file by searching for its name. |
| Ctrl + H | Find in whole project. (WebStorm uses the term "Find in "path".) |
| Edit > Find > Replace in Path | Replace in whole project. (Unfortunately, I can't find a keyboard shortcut for this common operation.) |
| Right-click > Refactor > Safe Delete | Allows you to delete a file |
| Right-click > Add to Favorites | Allows you to add files to a Favorites section, which expands below the list of files in the project pane. |

## Identifying changed files

When you have the Git and Github integration, changed files appear in blue. This lets you know what needs to be committed to your repository.

## Creating file templates

Rather than insert the frontmatter by hand each time, it's much faster to simply create a Jekyll template in WebStorm (my favorite editor for Jekyll projects).

To create a Jekyll template:

1. Right-click a file in the list of project files, and select **New > Edit File Templates**.

   If you don't see this option, you may need to create a file template first. Go to **File > Default Settings > Editor > File and Code Templates**. Create a new file template with an md extension, and then close and restart WebStorm. Then repeat this step and you will see the File Templates option appear in the right context menu.

2. In the upper-left corner of the dialog box that appears, click the **+** button to create a new template.
3. Name it Jekyll. Insert the frontmatter you want, and save it.

To use the Jekyll template, when you create a new file in your WebStorm project, you can select your Jekyll file template.