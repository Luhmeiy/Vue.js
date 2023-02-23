<template>
	<div id="main-banner">
		<h1>Make Your Burger</h1>
	</div>
</template>

<style lang="scss" scoped>
#main-banner {
	align-items: center;
	background-image: url("/img/burger.jpg");
	background-position: 0 -250px;
	background-size: cover;
	display: flex;
	height: 500px;
	justify-content: flex-start;

	& h1 {
		background-color: #222;
		color: #fff;
		font-size: 60px;
		padding: 20px 40px;
		text-align: center;
	}
}
</style>
