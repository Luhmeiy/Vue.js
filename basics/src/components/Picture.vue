<script lang="ts" setup>
import { ref } from "vue";
import ChangeImage from "./ChangeImage.vue";

const avatar = ref("/img/avatar.png");
const description = "Luiz H. Medeiros";

const changeImage = () => {
	avatar.value = "/img/avatar2.png";
};
</script>

<template>
	<img :src="avatar" :alt="description" />
	<ChangeImage @change-image="changeImage" />
</template>
