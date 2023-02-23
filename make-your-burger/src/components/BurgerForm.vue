<script lang="ts" setup>
import { onMounted, ref } from "vue";

interface DataProps {
	id: number;
	type: string;
}

let breads: DataProps[];
let meats: DataProps[];
let optionalData: DataProps[];

const name = ref<string | null>(null);
const bread = ref<string | null>(null);
const meat = ref<string | null>(null);
const optional = ref([]);

const isDataFetched = ref(false);

const getIngredients = async () => {
	const req = await fetch("http://localhost:3000/ingredients");
	const data = await req.json();

	breads = data.breads;
	meats = data.meats;
	optionalData = data.optional;

	isDataFetched.value = true;
};

const createBurger = async () => {
	const data = {
		name: name.value,
		meat: meat.value,
		bread: bread.value,
		optional: Array.from(optional.value),
		status: "Solicitado",
	};

	const dataJson = JSON.stringify(data);

	const req = await fetch("http://localhost:3000/burgers", {
		method: "POST",
		headers: {
			"Content-type": "application/json",
		},
		body: dataJson,
	});

	const res = await req.json();

	name.value = "";
	meat.value = "";
	bread.value = "";
	optional.value = [];
};

onMounted(getIngredients);
</script>

<template>
	<div>
		<div>
			<form
				id="burger-form"
				v-if="isDataFetched"
				@submit.prevent="createBurger"
			>
				<div class="input-container">
					<label for="name">Nome do cliente:</label>
					<input
						type="text"
						id="name"
						name="name"
						v-model="name"
						placeholder="Digite o seu nome"
					/>
				</div>

				<div class="input-container">
					<label for="bread">Escolha o pão:</label>
					<select name="bread" id="bread" v-model="bread">
						<option value="">Selecione o seu pão</option>
						<option v-for="bread in breads" :value="bread.type">
							{{ bread.type }}
						</option>
					</select>
				</div>

				<div class="input-container">
					<label for="meat">Escolha a carne do seu Burger:</label>
					<select name="meat" id="meat" v-model="meat">
						<option value="">Selecione o tipo de carne</option>
						<option v-for="meat in meats" :value="meat.type">
							{{ meat.type }}
						</option>
					</select>
				</div>

				<div class="input-container" id="optional-container">
					<label for="optional">Selecione os opcionais:</label>
					<div v-for="opt in optionalData" class="checkbox-container">
						<input
							type="checkbox"
							name="optional"
							id="optional"
							v-model="optional"
							:value="opt.type"
						/>
						<span>{{ opt.type }}</span>
					</div>
				</div>

				<div class="input-container">
					<input
						type="submit"
						value="Criar meu Burger"
						class="submit-btn"
					/>
				</div>
			</form>
		</div>
	</div>
</template>

<style lang="scss" scoped>
#burger-form {
	margin: 0 auto;
	max-width: 400px;
}

.input-container {
	display: flex;
	flex-direction: column;
	margin-bottom: 20px;

	label {
		border-left: 4px solid #fcba03;
		color: #222;
		font-weight: bold;
		margin-bottom: 15px;
		padding: 5px 10px;
	}

	input,
	select {
		padding: 5px 10px;
		width: 300px;
	}

	&#optional-container {
		flex-direction: row;
		flex-wrap: wrap;

		& label {
			width: 100%;
		}

		& .checkbox-container {
			align-items: flex-start;
			display: flex;
			margin-bottom: 20px;
			width: 50%;

			& span,
			& input {
				width: auto;
			}

			& span {
				font-weight: bold;
				margin-left: 6px;
			}
		}
	}

	& .submit-btn {
		background-color: #222;
		border: 2px solid #222;
		color: #fcba03;
		cursor: pointer;
		font-size: 16px;
		font-weight: bold;
		margin: 0 auto;
		padding: 10px;
		transition: 0.5s;

		&:hover {
			background-color: transparent;
			color: #222;
		}
	}
}
</style>
