<script lang="ts" setup>
import { onBeforeMount, onMounted, ref } from "vue";

const name = ref("Ainda não sei");

const lifeCycle = () => {
	console.log("Executou!");
};

onBeforeMount(() => {
	setTimeout(() => {
		name.value = "Medeiros";
	}, 1000);

	lifeCycle();
});

onMounted(() => {
	setTimeout(() => {
		name.value = "Luiz";
	}, 2000);

	lifeCycle();
});
</script>

<template>
	<h1>Meu nome é {{ name }}</h1>
</template>
