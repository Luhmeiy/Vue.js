<script lang="ts" setup>
import FirstComponent from "./components/FirstComponent.vue";
import LifeCycle from "./components/LifeCycle.vue";
import Person from "./components/Person.vue";
</script>

<template>
	<FirstComponent />
	<LifeCycle />
	<Person />
</template>

<script lang="ts">
export default {
	name: "App",
	components: {
		FirstComponent,
		LifeCycle,
		Person,
	},
};
</script>
