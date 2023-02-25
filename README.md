# weatherapp Notes

1. Initailly create vue app 
    - npm init @vue@latest
    - Choose the proper options
    - cd vue-project --> npm install --> npm run dev #to run the project on local host   

2. After Vue app created delete the unnescessary files
    assets / icons / App.vue / components / etc....

3. Setup tailwind css
    - Install Tailwind css
    - Tailwind config file - npx tailwindcss init -p
    - set template path 
4. Create tailwind.css file in assets, instal three main bases in that file. base, components, utilities
5. Customize tailwind in config file 
6. import it into main.js/ main.ts
7. tailwind.config.js 
    --> setup where to find the content that uses the tailwind css
    --> theme - extend - add css colors like primary, secondary etc...
    --> theme - fontfamily, container props, flex props  
8. For navigation use RouterLink
9. Use of reusable components, ref , emit, Teleport tag
10. V- Model for input tag (Search bar)
11. Creating Suspense tag when loading a component which has async data fetch (Lesson 8)
12. Create a City view component (Lesson 9)
13. Add city to local Storage (Lesson 10)
14. Retreive and display cities from local storage (Lesson 11)
15. 
16. Placeholder or spinner for data loading on the page (Lesson 12).
17. 
18. use beforeEach for router to set the titles dynamically for the webpages.
19. Deploy to netlify















# weatherapp

This template should help get you started developing with Vue 3 in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).

## Type Support for `.vue` Imports in TS

TypeScript cannot handle type information for `.vue` imports by default, so we replace the `tsc` CLI with `vue-tsc` for type checking. In editors, we need [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin) to make the TypeScript language service aware of `.vue` types.

If the standalone TypeScript plugin doesn't feel fast enough to you, Volar has also implemented a [Take Over Mode](https://github.com/johnsoncodehk/volar/discussions/471#discussioncomment-1361669) that is more performant. You can enable it by the following steps:

1. Disable the built-in TypeScript Extension
    1) Run `Extensions: Show Built-in Extensions` from VSCode's command palette
    2) Find `TypeScript and JavaScript Language Features`, right click and select `Disable (Workspace)`
2. Reload the VSCode window by running `Developer: Reload Window` from the command palette.

## Customize configuration

See [Vite Configuration Reference](https://vitejs.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Type-Check, Compile and Minify for Production

```sh
npm run build
```
