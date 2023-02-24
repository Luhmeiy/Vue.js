<script lang="ts" setup>
import { onMounted, ref } from "vue";
import Message from "./Message.vue";

interface BurgersData {
	id: number;
	name: string;
	meat: string;
	bread: string;
	optional: string[];
	status: string;
}

interface StatusData {
	id: number;
	type: string;
}

const burgers = ref<BurgersData[] | null>(null);
const status = ref<StatusData[]>([]);

const msg = ref<string | null>(null);

const getOrders = async () => {
	const req = await fetch("http://localhost:3000/burgers");
	const data = await req.json();

	burgers.value = data;

	getStatus();
};

const getStatus = async () => {
	const req = await fetch("http://localhost:3000/status");
	const data = await req.json();

	status.value = data;
};

const deleteBurger = async (id: number) => {
	const req = await fetch(`http://localhost:3000/burgers/${id}`, {
		method: "DELETE",
	});

	msg.value = `Pedido removido com sucesso`;
	setTimeout(() => (msg.value = ""), 3000);

	getOrders();
};

const updateBurger = async (event: Event, id: number) => {
	const option = (event.target as HTMLInputElement).value;

	const dataJson = JSON.stringify({ status: option });

	const req = await fetch(`http://localhost:3000/burgers/${id}`, {
		method: "PATCH",
		headers: { "Content-Type": "application/json" },
		body: dataJson,
	});

	const res = await req.json();

	msg.value = `O pedido Nº ${res.id} foi atualizado para ${res.status}`;
	setTimeout(() => (msg.value = ""), 3000);
};

onMounted(getOrders);
</script>

<template>
	<Message :msg="msg!" v-show="msg" />

	<div class="burger-table">
		<div>
			<div class="burger-table__heading">
				<div class="order-id">#:</div>
				<div>Cliente:</div>
				<div>Pão:</div>
				<div>Carne:</div>
				<div>Opcionais:</div>
				<div>Ações:</div>
			</div>
		</div>

		<div class="burger-table__rows">
			<div
				class="burger-table__row burger-table__row--big"
				v-for="burger in burgers"
			>
				<div class="order-number">{{ burger.id }}</div>
				<div>{{ burger.name }}</div>
				<div>{{ burger.bread }}</div>
				<div>{{ burger.meat }}</div>

				<div>
					<ul>
						<li v-for="opt in burger.optional">{{ opt }}</li>
					</ul>
				</div>

				<div class="controls">
					<select
						name="status"
						class="status"
						@change="($event) => updateBurger($event, burger.id)"
					>
						<option
							:value="stts.type"
							v-for="stts in status"
							:selected="burger.status === stts.type"
						>
							{{ stts.type }}
						</option>
					</select>

					<button class="delete-btn" @click="deleteBurger(burger.id)">
						Cancelar
					</button>
				</div>
			</div>

			<div
				class="burger-table__row burger-table__row--small"
				v-for="burger in burgers"
			>
				<div class="order-number">#{{ burger.id }}</div>

				<div>
					<b>Cliente</b>
					<p>{{ burger.name }}</p>
				</div>

				<div>
					<b>Pão</b>
					<p>{{ burger.bread }}</p>
				</div>

				<div>
					<b>Carne</b>
					<p>{{ burger.meat }}</p>
				</div>

				<div class="optional">
					<b>Opcionais</b>
					<ul>
						<li v-for="opt in burger.optional">{{ opt }}</li>
					</ul>
				</div>

				<div class="controls">
					<select
						name="status"
						class="status"
						@change="($event) => updateBurger($event, burger.id)"
					>
						<option
							:value="stts.type"
							v-for="stts in status"
							:selected="burger.status === stts.type"
						>
							{{ stts.type }}
						</option>
					</select>

					<button class="delete-btn" @click="deleteBurger(burger.id)">
						Cancelar
					</button>
				</div>
			</div>
		</div>
	</div>
</template>

<style lang="scss" scoped>
@mixin wrap {
	display: flex;
	flex-wrap: wrap;
}

@mixin div-width {
	& div {
		width: 19%;
	}
}

.burger-table {
	margin: 0 auto;
	max-width: 1200px;

	&__heading {
		border-bottom: 3px solid #333;
		font-weight: bold;
		padding: 12px;

		@include wrap;
		@include div-width;

		@media screen and (max-width: 850px) {
			display: none;
		}

		& .order-id {
			width: 5%;
		}
	}

	&__rows {
		@include wrap;
	}

	&__row {
		border-bottom: 1px solid #ccc;
		padding: 12px;
		width: 100%;

		&--big {
			@include wrap;
			@include div-width;

			@media screen and (max-width: 850px) {
				display: none;
			}

			& .controls {
				@media screen and (max-width: 1300px) {
					align-items: center;
					display: flex;
					flex-direction: column;
					row-gap: 10px;
				}
			}
		}

		&--small {
			align-items: flex-start;
			display: grid;
			grid-template-columns: repeat(3, 1fr);
			row-gap: 25px;

			@media screen and (min-width: 851px) {
				display: none;
			}

			@media screen and (max-width: 600px) {
				grid-template-columns: repeat(2, 1fr);
			}

			& .optional {
				@media screen and (min-width: 601px) {
					grid-column: 1 / 3;
				}
			}
		}
		& .order-number {
			width: 5%;

			@media screen and (max-width: 850px) {
				font-weight: bold;
				grid-column: 1 / -1;
			}
		}

		& ul {
			list-style-position: inside;
		}

		& .controls {
			display: flex;
			column-gap: 12px;

			@media screen and (max-width: 600px) {
				grid-column: 1 / -1;
				justify-self: center;
			}

			& select {
				padding: 12px 6px;
			}

			& .delete-btn {
				background-color: #222;
				border: 2px solid #222;
				color: #fcba03;
				cursor: pointer;
				font-size: 16px;
				font-weight: bold;
				padding: 10px;
				transition: 0.5s;

				&:hover {
					background-color: transparent;
					color: #222;
				}
			}
		}
	}
}
</style>
