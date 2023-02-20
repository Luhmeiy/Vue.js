<script lang="ts" setup>
import Form from "./Form.vue";
import Info from "./Info.vue";
</script>

<template>
	<h2>Essa é a descrição da pessoa: {{ name }}</h2>
	<Info />
	<Form />
</template>

<script lang="ts">
export default {
	name: "Person",
	components: {
		Info,
		Form,
	},
	data() {
		return {
			name: "Medeiros",
		};
	},
};
</script>
