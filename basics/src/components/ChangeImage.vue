<script lang="ts" setup>
defineEmits(["changeImage"]);
</script>

<template>
	<div>
		<button @click="$emit('changeImage')">Trocar imagem de perfil</button>
	</div>
</template>
