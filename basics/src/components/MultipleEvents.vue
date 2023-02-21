<script lang="ts" setup>
import { ref } from "vue";

const multiple_events = ref("");
const txt1 = "Primeiro evento";
const txt2 = "Segundo evento";

const first = (txt: string) => {
	multiple_events.value = `${txt} ativado!`;
};

const second = (txt: string) => {
	setTimeout(() => {
		multiple_events.value = `${txt} ativado!`;
	}, 500);
};

const third = () => {
	setTimeout(() => {
		multiple_events.value = "";
	}, 1500);
};
</script>

<template>
	<div>
		<button @click="first(txt1), second(txt2), third()">
			Ativar múltiplos eventos
		</button>
		<p>{{ multiple_events }}</p>
	</div>
</template>

<style scoped>
div {
	margin: 100px;
}
</style>
