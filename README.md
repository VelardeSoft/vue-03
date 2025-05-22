
# 🌐 Proyecto Vue + PrimeVue + Fake API

Este proyecto está configurado con Vue 3, PrimeVue, i18n, Vue Router y una Fake API REST utilizando `json-server`.

---

## 📁 Estructura Inicial del Proyecto

### Archivos de entorno

Crear en la raíz del proyecto:

```
.env.development
.env.production
```

### Contenido base para `.env`

```env
# Base de Path for Fake REST API
VITE_API_BASE_URL = http://localhost:3000
```

---

## 📂 Estructura dentro de `src/`

Crear las siguientes carpetas:

- `shared/`
- `layouts/`
- `pages/`
- `routes/`
- `translate/`

---

## 📦 Instalación de dependencias

Ejecutar los siguientes comandos:

```bash
npm i axios
npm install primevue @primeuix/themes
npm install vue-i18n@next
npm i vue-router
npm i json-server
```

---

## 📄 main.js

```js
import { createApp } from 'vue'
import './style.css'
import App from './App.vue'
import PrimeVue from 'primevue/config';
import Aura from '@primeuix/themes/aura';

// import i18n from '@/translate/i18n.js'
// import router from "@/routes/router.js";

import Button from 'primevue/button';

const app = createApp(App);

app.use(PrimeVue, {
    theme: {
        preset: Aura
    }
});

app.component('pv-button', Button);
// app.use(i18n)
// app.use(router)

app.mount('#app');
```

---

## 📁 shared > BaseServices.js

```js
import axios from 'axios'

export class BaseServices {
    static http = axios.create({
        baseURL: import.meta.env.VITE_API_BASE_URL
    })
}
```

---

## 📁 pages > the.response-error.component.vue

```vue
<script setup>
</script>

<template>
  <div class="not-found">
    <h1>404 Not Found</h1>
    <h2>Page under construction</h2>
  </div>
</template>

<style scoped>
.not-found {
  background-color: black;
  color: white;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: flex-start;
  padding: 20px;
}
</style>
```

---

## 🖼 Generación de Logo

Puedes generar un logo desde:

🔗 [https://www.logo.dev/dashboard/playground/logo-images](https://www.logo.dev/dashboard/playground/logo-images)

---

## 📁 layouts/

Crear los siguientes componentes:

- `main-layout.component.vue`
- `the-header.component.vue`
- `the-footer.component.vue`
- `the-sidebar.component.vue`

### 🧱 main-layout.component.vue

```vue
<template>
  <div class="layout">
    <the-header />
    <div class="main-content">
      <the-sidebar />
      <main class="content">
        <router-view></router-view>
      </main>
    </div>
    <the-footer />
  </div>
</template>

<script setup>
import TheHeader from './the-header.vue'
import TheFooter from './the-footer.vue'
import TheSidebar from './the-sidebar.vue'
</script>

<style scoped>
.layout {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}
.main-content {
  width: 100%;
  display: flex;
  flex: 1;
}
.content {
  flex: 1;
  padding: 20px;
}
</style>
```

### 🧱 the-header.component.vue

```vue
<template>
  <header class="header">
    <h1>Learning center</h1>
  </header>
</template>

<script setup></script>

<style scoped>
.header {
  background-color: #333;
  color: white;
  padding: 10px;
}
</style>
```

### 🧱 the-footer.component.vue

```vue
<template>
  <footer class="footer">
    <p>&copy; 2024 Your Company</p>
  </footer>
</template>

<script setup></script>

<style scoped>
.footer {
  background-color: #333;
  color: white;
  padding: 10px;
  text-align: center;
}
</style>
```

### 🧱 the-sidebar.component.vue

```vue
<template>
  <aside class="sidebar">
    <nav>
      <ul>
        <li><RouterLink to="/">Go to Home</RouterLink></li>
        <li><RouterLink to="/security">Security</RouterLink></li>
        <li><RouterLink to="/tutorial">Tutorial</RouterLink></li>
      </ul>
    </nav>
  </aside>
</template>

<script setup></script>

<style scoped>
.sidebar {
  width: 200px;
  background-color: #f4f4f4;
  padding: 15px;
}
.sidebar ul {
  list-style-type: none;
  padding: 0;
}
.sidebar ul li {
  margin: 10px 0;
}
.sidebar ul li a {
  text-decoration: none;
  color: #333;
}
</style>
```

---

## 📁 routes > router.js

```js
import { createRouter, createWebHistory } from "vue-router";

import LoginForm from '@/pages/LoginForm.vue'
import RegisterForm from '@/pages/RegisterForm.vue'
import NotFound from '@/pages/the.response-error.component.vue'

const routes = [
    { path: "/", component: LoginForm },
    { path: '/register', component: RegisterForm },
    { path: '/login', component: LoginForm },
    { path: '/:pathMatch(.*)*', name: 'NotFound', component: NotFound }
];

const router = createRouter({
    history: createWebHistory(),
    routes,
});

export default router;
```

---

## 📁 translate > i18n.js

```js
import { createI18n } from 'vue-i18n';

const messages = {
    es: {
        reservationHistory: {
            title: 'Historial de scooters alquilados',
            verDetalles: 'Ver Detalles'
        },
        reservationDetails: {
            title: 'Detalles de la reservación',
            fechaInicio: 'Fecha de inicio:'
        }
    },
    en: {
        reservationHistory: {
            title: 'Rental Scooter History',
            verDetalles: 'View Details'
        },
        reservationDetails: {
            title: 'Reservation Details',
            fechaInicio: 'Start Date:'
        }
    }
};

const i18n = createI18n({
    locale: 'es',
    fallbackLocale: 'es',
    messages
});

export default i18n;
```

---

## 📄 App.vue

```vue
<script setup>
</script>

<template>
  <router-view />
</template>
```

---

## 🔗 Enlaces en Sidebar

```vue
<template>
  <aside class="sidebar">
    <nav>
      <ul>
        <li><RouterLink to="/">Go to Home</RouterLink></li>
        <li><RouterLink to="/security">Security</RouterLink></li>
        <li><RouterLink to="/tutorial">Tutorial</RouterLink></li>
      </ul>
    </nav>
  </aside>
</template>
```

---

## 🛠 Tips de desarrollo

- Formatear código: `Ctrl + Alt + L`

---

## 🔄 Actualización de i18n

Si necesitas reemplazar una versión incorrecta de i18n:

```bash
npm uninstall i18n
npm install vue-i18n@next
```

---
