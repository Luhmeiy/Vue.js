<script lang="ts" setup>
import InputText from "./form/InputText.vue";
import Submit from "./form/Submit.vue";
</script>

<template>
	<h2>Meu Formulário:</h2>
	<InputText />
	<InputText />
	<Submit />
</template>

<script lang="ts">
export default {
	name: "Form",
	components: { InputText, Submit },
};
</script>
