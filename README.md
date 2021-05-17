# Front-End Web UI Frameworks and Tools: Bootstrap 4

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Front-End Web UI Frameworks and Tools: Bootstrap 4](#front-end-web-ui-frameworks-and-tools-bootstrap-4)
	- [Git](#git)
	- [Node.js and NPM](#nodejs-and-npm)
		- [Initializing package.json](#initializing-packagejson)
		- [Installing an NPM Module](#installing-an-npm-module)
		- [Setting up .gitignore](#setting-up-gitignore)
	- [CSS Preprocessors](#css-preprocessors)
		- [Less and Scss](#less-and-scss)
	- [NPM Scripts Part 1](#npm-scripts-part-1)
	- [Grunt and Gulp](#grunt-and-gulp)
		- [Creating a Grunt File](#creating-a-grunt-file)
		- [Compiling SCSS to CSS](#compiling-scss-to-css)
		- [Watch and Serve Tasks](#watch-and-serve-tasks)
	- [Useful Links](#useful-links)

<!-- /TOC -->

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

## NPM Scripts Part 1
`npm install --save-dev onchange@3.3.0 parallelshell@3.0.2`

`onchange` will watch changes for scss files and automatically compile css.
`parallelshell` will allow multiple npm scripts to be run simutaneously.

[Fixes for parallelshell](https://stackoverflow.com/a/53467253)

`npm install --save-dev rimraf@2.6.2`
`rimraf` cleans folder.

`npm -g install copyfiles@2.0.0`
`npm -g install imagemin-cli@3.0.0`
`npm install --save-dev usemin-cli@0.5.1 cssmin@0.4.3 uglifyjs@2.4.11 htmlmin@0.0.7`

`usemin` mins css, js and html

`gitignore` the `dist` folder

## Grunt and Gulp
### Creating a Grunt File
- Next you need to create a Grunt file containing the configuration for all the tasks to be run when you use Grunt. To do this, create a file named Gruntfile.js in the conFusion folder.
- Next, add the following code to Gruntfile.js to set up the file to configure Grunt tasks:
`npm install -g grunt-cli@1.2.0`
This sets up the Grunt module ready for including the grunt tasks inside the function above.

### Compiling SCSS to CSS
- Next, we are going to set up our first Grunt task. The SASS task converts the SCSS code to CSS. To do this, you need to include some Grunt modules that help us with the tasks. Install the following modules by typing the following at the prompt:

```
npm install grunt-sass@2.1.0 --save-dev
npm install time-grunt@1.4.0 --save-dev
npm install jit-grunt@0.10.0 --save-dev
```

The first one installs the Grunt module for SCSS to CSS conversion. The time-grunt module generates time statistics about how much time each task consumes, and jit-grunt enables us to include the necessary downloaded Grunt modules when needed for the tasks.

- Now, configure the SASS task in the Gruntfile as follows, by including the code inside the function in Gruntfile.js:

```
'use strict';

module.exports = function (grunt) {
    // Time how long tasks take. Can help when optimizing build times
    require('time-grunt')(grunt);

    // Automatically load required Grunt tasks
    require('jit-grunt')(grunt);

    // Define the configuration for all the tasks
    grunt.initConfig({
        sass: {
            dist: {
                files: {
                    'css/styles.css': 'css/styles.scss'
                }
            }
        }
    });

    grunt.registerTask('css', ['sass']);

};
```

- Now you can run the grunt SASS task by typing the following at the prompt:

`grunt css`

### Watch and Serve Tasks
- The final step is to use the Grunt modules watch and browser-sync to spin up a web server and keep a watch on the files and automatically reload the browser when any of the watched files are updated. To do this, install the following grunt modules:

```
npm install grunt-contrib-watch@1.0.0 --save-dev
npm install grunt-browser-sync@2.2.0 --save-dev
```
- After this, we will configure the browser-sync and watch tasks by adding the following code to the Grunt file:

```
,
        watch: {
            files: 'css/*.scss',
            tasks: ['sass']
        },
        browserSync: {
            dev: {
                bsFiles: {
                    src : [
                        'css/*.css',
                        '*.html',
                        'js/*.js'
                    ]
                },
                options: {
                    watchTask: true,
                    server: {
                        baseDir: "./"
                    }
                }
            }
        }s
```

- Then add the following task to the Grunt file:
`grunt.registerTask('default', ['browserSync', 'watch']);`

- Now if you type the following at the command prompt, it will start the server, and open the web page in your default browser. It will also keep a watch on the files in the css folder, and if you update any of them, it will compile the scss file into css file and load the updated page into the browser (livereload)

`grunt`

### Copying the Files and Cleaning Up the Dist Folder
- you will install the Grunt modules to copy over files to a distribution folder named dist, and clean up the dist folder when needed. To do this, install the following Grunt modules:

```
npm install grunt-contrib-copy@1.0.0 --save-dev
npm install grunt-contrib-clean@1.1.0 --save-dev
```

-You will now add the code to perform the copying of files to the dist folder, and cleaning up the dist folder. To do this, add the following code to Gruntfile.js. This should be added right after the configuration of the SASS task.:

```
,

        copy: {
            html: {
                files: [
                {
                    //for html
                    expand: true,
                    dot: true,
                    cwd: './',
                    src: ['*.html'],
                    dest: 'dist'
                }]                
            },
            fonts: {
                files: [
                {
                    //for font-awesome
                    expand: true,
                    dot: true,
                    cwd: 'node_modules/font-awesome',
                    src: ['fonts/*.*'],
                    dest: 'dist'
                }]
            }
        },

        clean: {
            build: {
                src: [ 'dist/']
            }
        }
```



## Useful Links
- [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
