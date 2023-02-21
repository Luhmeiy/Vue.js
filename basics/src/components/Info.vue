<script lang="ts" setup>
import { ref } from "vue";
import Picture from "./Picture.vue";

const show_email = ref(false);
const meu_link = "https://google.com";
const buttonText = ref("Mostrar email");
const backend_technologies = ["JavaScript", "PHP", "Python"];
const frontend_technologies = [
	{ id: 1, language: "HTML" },
	{ id: 2, language: "CSS" },
	{ id: 3, language: "Sass" },
];

const showEmail = () => {
	show_email.value = !show_email.value;

	if (!show_email.value) {
		buttonText.value = "Mostrar email";
	} else {
		buttonText.value = "Esconder email";
	}
};

defineProps({
	email: String,
	is_working: Boolean,
});
</script>

<template>
	<p v-if="is_working">Estou trabalhando no momento.</p>
	<p v-else>Estou em busca de novas oportunidades.</p>

	<p>Utilizo as seguintes tecnologias para backend:</p>
	<ul>
		<li v-for="technology in backend_technologies">{{ technology }}</li>
	</ul>

	<p>Utilizo as seguintes tecnologias para frontend:</p>
	<ul>
		<li v-for="technology in frontend_technologies">
			{{ technology.language }}
		</li>
	</ul>

	<div>
		<button @click="showEmail">{{ buttonText }}</button>
	</div>
	<p v-show="show_email">Mande uma mensagem para: {{ email }}</p>

	<p>
		Para acessar meu portfólio
		<a v-bind:href="meu_link" target="_blank">basta clicar aqui</a>
	</p>

	<Picture />
</template>
