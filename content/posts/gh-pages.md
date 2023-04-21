---
author: Sean Emerson
title: "Publishing an Astro site to Github Pages"
description: "Github pages offers free sites for github projects and organisations/users"
date: 2022-11-02
categories: [Astro]
tags: [npm, hosting, github-pages, astro]
---

The first step if you need to publish your site to github. There are two options:

- If you want an organisation/user site the repository name needs to be in the format `username.github.io` or `organizationname.github.io`
- If you want a project site then you can leave the repository name as-is. The url will be in the format `user.github.io/project` or `organization.github.io/project`

If you're using a free version of github, the repository needs to be public.

You need to ensure that you have initialized your project for git. If there is no `.git` folder, run the command `git init` to get started. You then need to crete a commit. The easiest option is to use Github Desktop and add a local repository. After you have created a commit, you can then publish the repository. Make sure you choose the correct organisation, if you are creating an organisation page. Remember you must make the repository public, unless you are on a paid github tier.

---

Before you can start with building and deployment there is a bug with Astro v2.0. All of the js and css resources are automatically bundled and placed in a `_astro` folder. Folders starting with `_` are disabled in Github Pages. Vite will at times generate assets starting with `_` which will also be disabled. 

Github Pages used jekyll to copy the files across to the server, and these files won't be copied, but there is an easy work around, although its a two step process so read carefully.

---

Step 1. Create a `.nojeykll` file in the `/public` directory - this file will end up in the root of your website.

Step 2. By default the `gh-pages` script below won't copy across 'dotfiles' so you need to add the `--dotfiles` option to your `gh-pages` script... see below!

---

It's now time to look at the tooling required to publish the site. To keep things simple we are going to use an NPM package, rather than setting up an automated process.

Install `gh-pages` with the command `npm install gh-pages`, or with the package manager of your choice.

You need to create some scripts - one to publish, and one which runs before publishing (to build the site). The following is an excerpt from the site's `package.json` file:

```json
{ 
  ...
  "scripts": {
    "dev": "astro dev",
    "start": "astro dev",
    "build": "astro build",
    "preview": "astro preview",
    "astro": "astro",
    "predeploy": "npm run build",
    "deploy": "gh-pages -d dist --branch gh-pages --dotfiles",
  },
...
}
```

- `-d dist` sets the source folder to `dist`
- `--branch gh-pages` copies the `dist` folder to the `gh-pages` branch
- `--dotfiles` enabled the copying of dotfiles, which is required so your `.nojeykll` file is copied across.. of your site will be broken!

The `predeploy` script runs before the deploy script, and simply builds the site to the `dist` folder (Astro default). When you run the `deploy` script, the site will be built, and then the `dist` folder will be copied to the `gh-pages` branch. This is committed automatically to your github repository.

So now that you have a copy of your built site in the `gh-pages` branch, you need to configure github to look out for it and publish whenever new files are uploaded.

When inside the repository on github, go to the `Settings` button, and then `Pages` on the left hand side menu.

Choose the following settings:

- Deploy from branch
- Branch: `gh-pages` `/(root)

If need be run `npm run deploy` again, and wait for your site to show up.
