<script lang="ts" setup>
defineProps({
	is_logged: Boolean,
});
</script>

<template>
	<ul>
		<li><a href="#">Home</a></li>
		<li><a href="#">Projetos</a></li>
		<li><a href="#">Contato</a></li>
		<li v-if="is_logged"><a href="#">Meu Perfil</a></li>
	</ul>
</template>

<style lang="scss" scoped>
ul {
	background-color: #111;
	display: flex;
	justify-content: center;
	list-style: none;

	& li {
		margin-right: 10px;

		& a {
			color: #ddd;
			text-decoration: none;
			transition: 0.5s;

			&:hover {
				color: turquoise;
			}
		}
	}
}
</style>
