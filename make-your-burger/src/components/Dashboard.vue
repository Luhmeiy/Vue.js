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
			<div class="burger-table__row" v-for="burger in burgers">
				<div class="order-number">{{ burger.id }}</div>
				<div>{{ burger.name }}</div>
				<div>{{ burger.bread }}</div>
				<div>{{ burger.meat }}</div>

				<div>
					<ul>
						<li v-for="opt in burger.optional">{{ opt }}</li>
					</ul>
				</div>

				<div>
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
.burger-table {
	margin: 0 auto;
	min-width: 750px;
	max-width: 1200px;

	&__heading,
	&__rows,
	&__row {
		display: flex;
		flex-wrap: wrap;
	}

	&__heading div,
	&__row div {
		width: 19%;
	}

	&__heading {
		border-bottom: 3px solid #333;
		font-weight: bold;
		padding: 12px;

		& .order-id {
			width: 5%;
		}
	}

	&__row {
		border-bottom: 1px solid #ccc;
		padding: 12px;
		width: 100%;

		& .order-number {
			width: 5%;
		}
	}

	& select {
		margin-right: 12px;
		padding: 12px 6px;
	}

	& .delete-btn {
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
