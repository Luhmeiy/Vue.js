<template>
	<div id="main-banner">
		<h1>Make Your Burger</h1>
	</div>
</template>

<style lang="scss" scoped>
#main-banner {
	align-items: center;
	background-image: url("/img/burger.jpg");
	background-position: 0 50%;
	background-size: cover;
	display: flex;
	height: 400px;
	justify-content: flex-start;

	@media screen and (max-width: 600px) {
		height: 200px;
	}

	& h1 {
		background-color: #222;
		color: #fff;
		font-size: 60px;
		padding: 20px 40px;
		text-align: center;

		@media screen and (max-width: 600px) {
			font-size: 30px;
			padding: 10px 20px;
		}
	}
}
</style>
