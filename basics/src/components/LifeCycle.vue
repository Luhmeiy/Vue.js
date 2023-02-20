<template>
	<h1>Meu nome é {{ name }}</h1>
</template>

<script lang="ts">
export default {
	name: "LifeCycle",
	data() {
		return {
			name: "Ainda não sei",
		};
	},
	created() {
		setTimeout(() => {
			this.name = "Medeiros";
		}, 1000);
	},
	mounted() {
		setTimeout(() => {
			this.name = "Luiz";
		}, 2000);
	},
};
</script>
