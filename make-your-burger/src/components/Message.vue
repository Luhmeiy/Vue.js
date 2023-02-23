<script lang="ts" setup>
defineProps({
	msg: String,
});
</script>

<template>
	<div class="message-container">
		<p>{{ msg }}</p>
	</div>
</template>

<style scoped>
.message-container {
	background-color: #cce5ff;
	border: 2px solid #b8daff;
	border-radius: 5px;
	color: #004085;
	margin: 30px auto;
	max-width: 400px;
	padding: 10px;
}
</style>
