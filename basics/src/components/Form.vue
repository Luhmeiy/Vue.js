<script lang="ts" setup>
import { ref } from "vue";
import InputText from "./form/InputText.vue";
import Submit from "./form/Submit.vue";

const name = ref("");
const email = ref("");

const submitForm = () => {
	console.log("Formulário enviado!");
	console.log(`O nome é ${name.value}`);
	console.log(`O email é ${email.value}`);

	name.value = "";
	email.value = "";
};
</script>

<template>
	<h2>Meu Formulário:</h2>

	<form @submit.prevent="submitForm">
		<input type="text" v-model="name" />
		<input type="email" v-model="email" />
		<Submit />
	</form>
</template>
