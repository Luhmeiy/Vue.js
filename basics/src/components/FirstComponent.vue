<template>
	<h1>Olá Vue!</h1>
	<p>Meu nome é {{ name }} e trabalho com {{ role }}</p>
</template>

<script lang="ts">
export default {
	name: "FirstComponent",
	data() {
		return {
			name: "Medeiros",
			role: "Programador",
		};
	},
};
</script>
