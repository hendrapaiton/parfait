# About this project

This project is a template for constructing a Laravel project that supports Vite Vue Typescript. This project serves as a case study for students learning Laravel and SPA at a Vocational High School.


## Practices in Steps

#### Create New Project

First, create new laravel project with composer and make sure you have installed php and composer in your system.

```bash
composer global require laravel/installer
laravel new <projectname>
```

Choose none for No staterkit.

```bash
would you like to install a starter kit?
[none     ] No starter kit
[breeze   ] Laravel Breeze
[jetstream] Laravel Jetstream
> none
```

Choose 0 PHPunit for teseting framework.

```bash
[0] PHPUnit
[1] Pest
> 0
```
Choose yes to initialize git repository.

```bash
Would you like to initialize a Git repository? (yes/no) [no]:
> yes
```
Choose MySQL for database in my application.

```bash
Which database will your application use? [MySQL]:
[mysql ] MySQL
[pgsql ] PostgreSQL
[sqlite] SQLite
[sqlsrv] SQL Server
>
```

### Add typescript support

Install Typescript with NPM. Change vite.config.js to vite.config.ts and then add configuration as follows.

```ts
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';
import vue from '@vitejs/plugin-vue';

export default defineConfig({
    plugins: [
        laravel({
            input: ['resources/js/app.ts'],
            refresh: true,
        }),
        vue({
            template: {
                transformAssetUrls: {
                    base: null,
                    includeAbsolute: false,
                },
            },
        }),
    ],
});
```
Delete ```bootstrap.js``` in ```resources/js/``` and change ```app.js``` to ```main.ts```. And then load ```vue``` in ```main.ts``` with ```createdApp``` and add ```App``` component to application.

```ts
import { createApp } from 'vue';
import App from './App.vue';

createApp(App).mount('#app');
```

Make a html document in a new file ```main.blade.php``` and add Typescript to the document.
And don't forget to div element with ```id="app"```.

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Laravel SPA with Typescript Vue</title>
</head>

<body>
    <div id="app"></div>
    @vite('resources/js/main.ts')
</body>

</html>

```

Route ```main.blade.php``` to ```web.php``` and change path ```/``` to ```main```.
```ts

Route::get('/', function () {
    return view('main');
});
```

Last but not least. Insert Typescript to tempalate in App.vue to show the value of ```salam```.

```ts
<template>
  {{ salam }}
</template>

<script setup lang="ts">
import { ref } from 'vue';

const salam = ref('Halu Dunia');
</script>
```
