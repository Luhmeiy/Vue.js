<script lang="ts" setup>
import FirstComponent from "./components/FirstComponent.vue";
import Header from "./components/Header.vue";
import LifeCycle from "./components/LifeCycle.vue";
import Person from "./components/Person.vue";
</script>

<template>
	<Header :is_logged="true" />
	<FirstComponent />
	<LifeCycle />
	<Person />
</template>

<style>
a {
	color: red;
}
</style>
