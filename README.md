# Todo-Vue-Typescript

This is the TypeScript version of the TodoMatic tutorial project for Vue.js on [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Vue_getting_started). This project was bootstrapped with [Vue CLI](https://cli.vuejs.org/).

There are some changes:

* Use Composition API instead of Optional API for all Vue components.
* This version adds buttons to switch all/active/completed items just like the [React](https://github.com/alankrantas/todo-react-typescript) version. A *FilterButton* component is added.
* Use icons on buttons and the item would be crossed out if "completed".

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