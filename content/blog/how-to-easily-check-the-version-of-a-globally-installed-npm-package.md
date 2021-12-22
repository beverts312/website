---
date: 2017-03-17
title: "How to easily check the version of a globally installed npm package"
author: Bailey Everts
---

### Why

When opening an issue on github, it is important to provide all the relevant information to your bug, one of those things being the version of the package you are having trouble with. We wanted to provide users of the [swellaby yeoman generator](https://github.com/swellaby/generator-swell) an easy way to retrieve the version of their generator so I made a small utility to help with that, which can be used on any globally installed package.

### How

Assuming you have node & npm installed (how else would you have a globally installed npm package), here are the steps:

1. Install my utility npm install -g get-pkg-version.
2. Use it get-pkg-version <package-name>
3. You can test it out with the package itself get-pkg-version get-pkg-version.

You can check out the source code [here](https://github.com/swellaby/get-package-version).