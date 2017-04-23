# Installing and running a package with NPM

## What is NPM?

A command line program to download and manage NodeJS packages that have been published to the web.

More generally - code written by others that you can use in your own project.

## Global NPM packages

Use it to install system-wide tools that you'll need in each and every project (such as `http-server`).

```
npm install -g <package-name>
```

## Local packages

Most packages will be local - its the tools/code that your project needs to work.

In order to be able to use NPM effectively in your project the first step is to tell NPM that your project will use NPM to manage its dependecies.

In the root of your project folder write:
```
npm init
```
This will create a `package.json` file that will contain all the NPM related info for your project.

Now you can install the package locally in your project and save as a dependency:

```
npm install --save <package-name>
```

Checkout the `"dependencies"` section in `package.json` and see that the package was added there.

## Run a package (`node-sass` example)

If your package is a command line tool (like `node-sass`) it'll be convenient to create a simple script alias to run it.

In the `"scripts"` section in `package.json` add:
```
"scripts": {
  "sass": "node-sass --watch path/to/styles.scss path/to/styles.css"
}
```

Now you can write in the root of your project folder:
```
npm run sass
```
And the `node-sass` script will run from the `node_modules` folder as if its in the PATH.
