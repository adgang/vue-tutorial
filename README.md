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

## 2. Create a Vue project
> vue init webpack <project-name>

I chose the webpack template here. There are other options available. The init command creates a Vue app and a component called Hello, with a route path `/` assigned to it. You can run
> npm run dev

to check that the app is running. Be sure to run `npm install` before running the app. Change the port in `config/index.js` if necessary. I changed it to 18080.

## 3. Getting the App working

To understand how the app is working check the following files in that order.
```
index.html => The single page application's, well, single page.
src/main.js => The main javascript file which creates a Vue object(App) and binds it to a div on the page. Also defines where to find routes(./router).
src/App.vue => The vue file which defines the template and logic to inject page specific stuff based on path. The `router-view` element will inject the stuff from the relevant Vue component.
src/router/index.js => Defines routes mapping Controllers to paths
src/components/Hello.vue => The Hello component which renders the welcome message and all the links.
```

First run `npm run dev`
Keep `localhost:18080` open on a browser.
Let us customize stuff a bit. Let's replace the welcome message in Hello.vue with:
>   Welcome to My Vue.js Tutorial App

Magically the browser will change its welcome message in a split second. Vue's tooling takes care of the update as long as `npm run dev` is running. The update is definitely way faster than in Angular.

## 4. Writing a new component

  Now lets try and hit the page `http://localhost:18080/#/about` in browser. Obviously there is no route mapped to the path. So all you see would be the Vue logo. This becomes apparent from the check list of files above. The router-view is not able to render anything for this path, so the page only shows the logo which is rendered by the App directly.

Now its time to write a new component which will render something when we hit the about url `/about`. If you had examined the files in the above checklist, it is easy to guess what to change. The steps are simple:

#### a. Assign a route:

Add a new route in `src/route/index.js`
```
 {
   path: '/about',
   name: 'About',
   component: About
 }
```
 #### b. Write a new component:
 Obviously the router will not be able to find the component called About. So we write a new file called About.vue in `src/components` with the following contents.

 ```
 <template>
   <div class="about">
     <h1>{{ msg }}</h1>
   </div>
 </template>
 <script>
 export default {
   name: 'about',
   data () {
     return {
       msg: 'This is the About page. Really its just a fun experimental app'
     }
   }
 }
 </script>
 ```

Now the `localhost:18080/#/about` page shows the line about our app. Why is the hideous # in our path? Wait, is it not possible to get clean old path like `localhost:18080/about` for our page?! For that just make the router use [history mode](https://router.vuejs.org/en/essentials/history-mode.html). But history mode comes with its own quirks. Be sure to stich up things for using such paths. We will continue our tutorial in the default mode(called hash mode after the hideous hash).

## 5. Composing Components
Vue offers amazingly powerful ways to compose components(use one component in another). It's simplicity is like a fresh breathe of air coming from Angular world. Here let us try using the About component in our home page component(Hello component). All we have to do is tell Hello component that we are going to use the About component from so-and-so file using a custom element(similar to directive in Angular). And the simply use the custom element in the component template.

So in the script section of Hello.vue, we import About and include it in components used by Hello like so:
```
<script>
import About from './About'
export default {
  name: 'hello',
  components: { 'about': About },
  data () {
  ...
</script>
```
Now we can use <about> element in Hello's template as many times as we want:
```
<template>
  <div class="hello">
    ...
    <about></about>
    <about></about>
  </div>
</template>
```
And we already can see two identical `about` messages. But they are both showing the same boring message. What is the point of having subcomponents(called child components in documentation) if they can only ever bind to same data? It's like a class whose instances have all the same data. This is why Vue provides props.

On a small detour, the Vue philosophy is [props down, events up](https://vuejs.org/v2/guide/components.html#Composing-Components) which means child components receive props from parents and then emit events back to parents. Thats it! A child cannot(or rather should not) access parent's data.

So now we have to make our parent Hello component set props of About child components. Two steps:

a. First, `About` component should explicitly declare the props it accepts. In About.vue, lets make `msg` a prop.
```
<script>
export default {
  name: 'about',
  props: ['msg'],
  data () {
  ...
}
</script>
```

b. The parent Hello component should pass on the prop values for each child component. In Hello.vue where we show about component, pass on msg as needed.
```
<template>
  <div class="hello">
    ...
    <about msg='This is about the first child component'></about>
    <about msg='This is about the second child'></about>
    <about></about>
  </div>
</template>
```

That's it we have resused a component within another.


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
