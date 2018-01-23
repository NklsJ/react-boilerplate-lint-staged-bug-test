# Test lint staged bug

Created from https://github.com/digiaonline/react-boilerplate

## What's wrong?

Seems like lint-staged doesn't work correctly if you add 2 css files into commit, if both or one of those files need linting.
Lint-staged stages both files with the content of just one file overwriting the changes.

## Steps to reproduce the bug

- Install Yarn globally (if you haven't yet) https://yarnpkg.com/lang/en/docs/install/
- Clone this repo
- Change contents of `src/hello/components/Hello.css` so that the file has css lint errors (add too much indent for example)
- Change contents of `src/root/components/Root.css` so that the file has css lint errors (add too much indent for example)
- Type `git add .`
- Type `yarn precommit`
- Open both css files. One of the files should have been overwritten with the content from the other file.


## Steps to fix the bug

This issue seems to fix itself if you modify `.lintstagedrc` to this

````
{
  "*.js": [
    "prettier-eslint --write \"src/**/*.js\"",
    "git add"
  ],
  "*.css": [
    "stylefmt --recursive",
    "git add"
  ]
}
````

So if you add `--recursive` to this line `"stylefmt --recursive",`

More discussion on the topic here https://github.com/okonet/lint-staged/issues/164
