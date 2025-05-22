# Pasos para Configurar un Proyecto Vue.js

---

Este README.md resume los pasos clave para configurar y estructurar un proyecto Vue.js, incluyendo la gestión de variables de entorno, la integración de librerías y la configuración de rutas y servicios.

## 1. Configuración de Entorno

---

### Variables de Entorno

Crea archivos de entorno en la raíz de `src` para manejar diferentes configuraciones:

-   **`.env.development`**
-   **`.env.production`**

Dentro de cada archivo, define la URL base para tu API, por ejemplo:

VITE_API_BASE_URL = http://localhost:3000


## 2. Estructura de Carpetas en `src`

---

Organiza tu código en carpetas lógicas dentro de `src`:

-   **`shared`**: Para archivos compartidos como la configuración de servicios.
-   **`pages`**: Para los componentes de tus vistas principales.
-   **`layouts`**: Para la estructura general de la aplicación (encabezado, pie de página, barra lateral).
-   **`routes`**: Para la configuración del enrutador de Vue.
-   **`translate`**: Para la configuración de internacionalización (i18n).

## 3. Instalación de Dependencias

---

Instala las librerías necesarias para el proyecto:

```bash
npm i axios
npm install primevue @primeuix/themes
npm i vue-router
npm i json-server
npm install vue-i18n@next # Reemplaza 'npm i i18n' por esta versión

## 4. Configuración Principal de Vue (main.js)
Configura la aplicación Vue, incluyendo PrimeVue y los componentes globales. Descomenta las líneas de i18n y router una vez que los archivos estén configurados.

JavaScript

import { createApp } from 'vue'
import './style.css'
import App from './App.vue'
import PrimeVue from 'primevue/config';
import Aura from '@primeuix/themes/aura';

import i18n from '@/translate/i18n.js' // Asegúrate de que la ruta sea correcta
import router from "@/routes/router.js"; // Asegúrate de que la ruta sea correcta

import Button from 'primevue/button';

const app = createApp(App);
app.use(PrimeVue, {
    theme: {
        preset: Aura
    }
});
app.component('pv-button', Button);
app.use(i18n)
app.use(router)
app.mount('#app');

## 5. Configuración de Servicios Base (shared/BaseServices.js)
Crea un servicio base para manejar las solicitudes HTTP usando Axios:

JavaScript

import axios from 'axios'
export class BaseServices {
    static http = axios.create({
        baseURL: import.meta.env.VITE_API_BASE_URL
    })
}

## 6. Componentes de Páginas y Layouts
Página de Error (pages/the.response-error.component.vue)
Un componente básico para manejar errores 404:

Fragmento de código

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
Componentes de Layout (layouts/)
layouts/main-layouts.component.vue
Define la estructura principal de la aplicación, integrando el encabezado, pie de página y barra lateral.

Fragmento de código

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
layouts/the-header.component.vue
Fragmento de código

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
layouts/the-footer.component.vue
Fragmento de código

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
layouts/the-sidebar.component.vue
Fragmento de código

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

## 7. Configuración de Rutas (routes/router.js)
Define las rutas de tu aplicación utilizando Vue Router:

JavaScript

import { createRouter, createWebHistory } from "vue-router";
import LoginForm from '@/pages/LoginForm.vue'; // Asegúrate de tener estos componentes
import RegisterForm from '@/pages/RegisterForm.vue'; // Asegúrate de tener estos componentes
import NotFound from '@/pages/the.response-error.component.vue'; // Usa tu componente de error

const routes = [
    { path: "/", component: LoginForm },
    { path: '/register', component: RegisterForm },
    { path: '/login', component: LoginForm },
    { path: '/:pathMatch(.*)*', name:'NotFound', component: NotFound }
];

const router = createRouter({
    history: createWebHistory(),
    routes,
});
export default router;

## 8. Configuración de Internacionalización (translate/i18n.js)
Configura vue-i18n para manejar múltiples idiomas en tu aplicación:

JavaScript

import { createI18n } from 'vue-i18n';

const messages = {
    es: {
        reservationHistory: {
            title: 'Historial de scooters alquilados',
            verDetalles: 'Ver Detalles'
        },
        reservationDetails: {
            title: 'Detalles de la Reserva',
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

## 9. Componente Raíz (App.vue)
El componente principal de tu aplicación, donde se renderizan las rutas:

Fragmento de código

<script setup>
</script>

<template>
  <router-view />
</template>

## 10. Atajos Útiles
Formatear código: Ctrl + Alt + L
