# Todo-Vue-Typescript

This is the TypeScript version of the TodoMatic tutorial project for Vue.js on [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Vue_getting_started). This project was bootstrapped with [Vue CLI](https://cli.vuejs.org/).

There are some changes:

* Use Composition API instead of Optional API for all Vue components.
* This version add a *FilterButton* component to get the all/active/completed item filtering just like the [React](https://github.com/alankrantas/todo-react-typescript) version.
* Some tweak of styles, use icons on buttons and the item would be crossed out if "completed".

![vue](https://user-images.githubusercontent.com/44191076/167265259-bf5e1bde-9ce7-4dfa-9877-7392e8c5ded3.png)

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

### Run Local Server (Run Build First)

```
npm install -g http-server
http-server ./dist
```
