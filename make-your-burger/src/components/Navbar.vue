<script lang="ts" setup>
defineProps({
	logo: String,
	alt: String,
});
</script>

<template>
	<div id="nav">
		<router-link to="/" id="logo_url">
			<img :src="logo" :alt="alt" id="logo" />
		</router-link>
		<router-link to="/">Home</router-link>
		<router-link to="/pedidos">Pedidos</router-link>
	</div>
</template>

<style lang="scss" scoped>
#nav {
	align-items: center;
	background-color: #222;
	border-bottom: 4px solid #111;
	display: flex;
	justify-content: flex-end;
	padding: 15px 50px;

	& #logo_url {
		margin: auto;
		margin-left: 0;

		& #logo {
			height: 40px;
			width: 40px;
		}
	}

	& a {
		color: #fcba03;
		margin: 12px;
		text-decoration: none;
		transition: 0.5s;

		&:hover {
			color: #fff;
		}
	}
}
</style>
