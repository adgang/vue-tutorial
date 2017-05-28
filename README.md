# vue-tutorial

> A sample step by step, commit by commit Vue tutorial. We are really only looking to learn writing a simple app using vue-cli. The following are the things we demo in each commit.

1. vue-cli installation
2. Creating a vue project
3. Getting the root controller or the controller on path `/` running with an App.
4. Writing a simple Component and assign a route to it.
5. Writing two components and using composition(using one component in another).

## 1. vue-cli installation
First, we global install vue-cli like so:
> npm install -g vue-cli

Depending on your npm setup, you might need sudo on above command.

## 2. Create a vue project
> vue init webpack <project-name>

I chose the webpack template here. There are other options available. The init command creates a Vue app and a component called Hello, with a route path `/` assigned to it. You can run
> npm run dev

to check that the app is running.



## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report

# run unit tests
npm run unit

# run e2e tests
npm run e2e

# run all tests
npm test
```

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
