>navigated to server in browser

- obvious broken config from index of base url
>investigate source of html

- images being sourced from wrong domain, so we edit it to see if it can source file locally

> yes file is available locally, and its an image, so lets navigate to resource directly

- directory traversal, find that directories are visible to end user
- /theme/Innovation/assets/images/break.png

> google used to lookup 