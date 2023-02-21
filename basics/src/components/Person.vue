<script lang="ts" setup>
import Form from "./Form.vue";
import Info from "./Info.vue";

const name = "Medeiros";
const email = "teste-novo@teste.com";
</script>

<template>
	<h2>Essa é a descrição da pessoa: {{ name }}</h2>
	<Info :email="email" :is_working="false" />
	<Form />
</template>
