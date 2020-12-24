# Bravado quest

Implement a simple profile search application using Vue. See it live [here]{https://bravado-quest.netlify.app/}.

## Layout design

Can be found here: https://www.figma.com/file/PyncPYa1rpOxRooTdfvgxHRN/Bravado-Quest

## Steps

Application is running on a project root (`/`). The sample data to use inside application is taken using an AJAX call from the Star Wars API by [Akabab](https://akabab.github.io/starwars-api).

The default app state contains all profile cards. When user starts typing, the results are filtered in realtime, highlighting the matching string.

## Highlights

- General SPA application performance, including searching, scrolling and highlighting speed.
- Quality of Vue single file components (SFC)
- HTML(JSX) and CSS quality
- JS code quality
- Search should be stateful (using browser url e.g. `/search/Boris`)
- Application should be published online for testing purposes
- Changes should be published in a fork

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
