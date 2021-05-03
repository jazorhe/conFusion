# Front-End Web UI Frameworks and Tools: Bootstrap 4

## Git
`git init`

`git status`

`git add .`

`git commit -m "first commit"`

`git log --oneline`

`git checkout <second commit's number> index.html`

`git reset HEAD index.html`

`git checkout -- index.html`

`git remote add origin <repository URL>`

`git push -u origin master`

`git clone <repository URL>`


## Node.js and NPM
<https://nodejs.org>
```
node -v

npm -v
```
### Initializing package.json
- At the command prompt in your `git-test` folder, type

`npm init`

- Follow along the prompts and answer the questions as follows: accept the default values for most of the entries, except set the entry point to index.html
- This should create a package.json file in your git-test folder.

### Installing an NPM Module

- Install an NPM module, lite-server, that allows you to run a Node.js based development web server and serve up your project files. To do this, type the following at the prompt:

`npm install lite-server --save-dev`

- You can check out more documentation on lite-server here.
- Next, open package.json in your editor and modify it as shown below. Note the addition of two lines, line 7 and line 9.

```
{
  "name": "git-test",
  "version": "1.0.0",
  "description": "This is the Git and Node basic learning project",
  "main": "index.html",
  "scripts": {
    "start": "npm run lite",
    "test": "echo \"Error: no test specified\" && exit 1",
    "lite": "lite-server"
  },
  "repository": {
    "type": "git",
    "url": "git+https://jogesh_k_muppala@bitbucket.org/jogesh_k_muppala/git-test.git"
  },
  "author": "",
  "license": "ISC",
  "homepage": "https://bitbucket.org/jogesh_k_muppala/git-test#readme",
  "devDependencies": {
    "lite-server": "^2.2.2"
  }
}
```
- Next, start the development server by typing the following at the prompt:
`npm start`

- This should open your index.html page in your default browser.
- If you now open the index.html page in an editor and make changes and save, the browser should immediately refresh to reflect the changes.

### Setting up .gitignore
- Next, create a file in your project directory named .gitignore (Note: the name starts with a period)Then, add the following to the .gitignore file
`node_modules`

- Then do a git commit and push the changes to the online repository. You will note that the node_modules folder will not be added to the commit, and will not be uploaded to the repository.

## CSS Preprocessors
### Less and Scss
`npm install -g less@2.7.2`

`lessc styles.less styles.css`
