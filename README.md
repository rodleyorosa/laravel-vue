# laravel-vue

## Metodi principali di implementazione vue-laravel
Esistono principalmente due metodi per utilizzare Vue.js con Laravel:
1. Metodo manuale: In questo metodo, si deve creare manualmente l'ambiente per l'utilizzo di Vue.js all'interno di un'applicazione Laravel. Questo include l'installazione del pacchetto Vue.js, l'inclusione dei file JavaScript di Vue.js e la definizione dei componenti Vue.js. Questo metodo è consigliato se si vuole avere un maggiore controllo sull'implementazione e sulla personalizzazione dell'applicazione.
2. Metodo di scaffolding: Laravel include un comando di scaffolding (php artisan ui vue) che consente di installare e configurare automaticamente Vue.js all'interno di un'applicazione Laravel, compreso il sistema di autenticazione. Questo metodo è consigliato se si vuole un'implementazione più rapida e standardizzata, ma potrebbe essere meno flessibile in termini di personalizzazione.

In entrambi i metodi, l'utilizzo di Vue.js all'interno di Laravel richiede la conoscenza di entrambe le tecnologie e delle loro interazioni.

## NPM
Per utilizzare Vue.js in un'applicazione Laravel, è necessario installare i seguenti pacchetti NPM:
1. vue: questo è il pacchetto principale di Vue.js, che fornisce la libreria JavaScript per la gestione delle interfacce utente reactive.
2. vue-template-compiler: questo pacchetto consente di compilare i template Vue.js in JavaScript. Viene utilizzato da Laravel Mix durante la compilazione dei file front-end.
3. laravel-mix: se si utilizza Laravel, questo pacchetto semplifica la compilazione dei file front-end, tra cui i file CSS, JavaScript e Vue.js. Tuttavia, non è strettamente necessario per l'utilizzo di Vue.js
4. @vitejs/plugin-vue

## Files
- resources/app.js
```js
import { createApp } from 'vue';
import './bootstrap';
import ExampleComponent from './components/ExampleComponent.vue'

const app = createApp({})

app.component('example-component', ExampleComponent)
app.mount('#app')
```
- vite.config.js
```js
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';
import vue from '@vitejs/plugin-vue'

export default defineConfig({
    plugins: [
        laravel({
            input: ['resources/css/app.css', 'resources/js/app.js'],
            refresh: true,
        }),
        vue()
    ],
    resolve: {
        alias: {
            vue: 'vue/dist/vue.esm-bundler.js',
        },
    },
});
```
- welcome.blade.php

```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    @vite('resources/js/app.js')
</head>
<body>
    <div id="app">
        <example-component></example-component>
    </div>
</body>
</html>

```
