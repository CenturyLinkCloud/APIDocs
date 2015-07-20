CenturyLink Cloud API Documentation
========

### Links (API doc to API doc)


Links to other articles should follow this format:

```
[Link Text](../category/api-doc-name.md)
```
 
so like this (folder names are case-sensitive):

```
[API v2.0 Overview](../Getting Started/api-v2-overview.md)
[Login](../Authentication/login.md )
```

### Commit Analyzer

This repository contains a [commit analyzer](https://github.com/thenickcox/commit_analyzer) that runs against each file in the repository validating that the following are true:

* File's JSON front-matter parses correctly and contains the required fields (title, date, autor)
* File's markdown successfully parses
* All relative files (images and other markdown files) are valid links

To run this check locally, `cd` into the root of this project and run:

```shell
node lib/index.js
```

The output will tell you if any file fails parsing. This script is also run as part of continuous integration with [travis-ci](http://travis-ci.org).
