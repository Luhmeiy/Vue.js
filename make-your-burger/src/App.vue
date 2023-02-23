<script setup lang="ts">
import Footer from "./components/Footer.vue";
import Navbar from "./components/Navbar.vue";

const logo_src = "/img/logo.png";
const app_name = "Make your Burger";
</script>

<template>
	<Navbar :logo="logo_src" :alt="app_name" />
	<router-view />
	<Footer />
</template>
