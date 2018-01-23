# Test lint staged bug

Created from https://github.com/digiaonline/react-boilerplate

## What's wrong?

Seems like lint-staged doesn't work correctly if you add 2 css files into commit, if both those files need linting.
Lint-staged stages both files with the content of just one file.

## Steps to reproduce the bug

- Install Yarn globally (if you haven't yet) https://yarnpkg.com/lang/en/docs/install/
- Clone this repo
- Change contents of `src/hello/components/Hello.css` so that the file has css lint errors (add too much indent for example)
- Change contents of `src/root/components/Root.css` so that the file has css lint errors (add too much indent for example)
- Type `git add .`
- Type `yarn precommit`
- Open both css files. One of the files should have been overwritten with the content from the other file.
