# WeatherApp

Is it good for laundry today👕 or maybe help you from getting drenched in the rain ⛈️. How you say?? 

Introducing the all new WeatherApp. Yeah that's right, this app will give you weather updates saves your day 🌈. Keeps you prepared against the bad weather ☂️.

This app is built using Vue JS 💚.

Hi there,

The app is built as a part of learning and understanding Vue JS framework.
Playlist I followed - https://www.youtube.com/playlist?list=PL4cUxeGkcC9hfoy8vFQ5tbXO3vY0xhhUZ

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
    - setup where to find the content that uses the tailwind css
    - theme - extend - add css colors like primary, secondary etc...
    - theme - fontfamily, container props, flex props  

8. For navigation use RouterLink

9. Use of reusable components, ref , emit, Teleport tag

10. V- Model for input tag (Search bar)

11. Creating Suspense tag when loading a component which has async data fetch (Lesson 8)

12. Create a City view component (Lesson 9)

13. Add city to local Storage (Lesson 10)

14. Retreive and display cities from local storage (Lesson 11)

15. Placeholder or spinner for data loading on the page (Lesson 12).

16. use beforeEach for router to set the titles dynamically for the webpages.

17. Deploy to netlify

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).

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

Thank you for checking out my repo.
