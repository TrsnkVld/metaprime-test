<template>
	<div class="sort-list">
		<div class="sort-list__header">
			<button
				@click="sortById()"
				class="btn"
				:class="{ active: !activeBtn }"
			>
				ID
			</button>
			<button
				@click="sortByName()"
				class="btn"
				:class="{ active: activeBtn }"
			>
				Имя
			</button>
		</div>
		<table v-if="list.length" class="sort-list__table">
			<tr v-for="item in list" :key="item.id">
				<td>
					<input v-model="item.checked" type="checkbox" />
				</td>
				<td>{{ item.id }}</td>
				<td>{{ item.name }}</td>
			</tr>
		</table>
		<div v-else class="sort-list__message">Список пуст</div>
	</div>
</template>

<script>
export default {
	name: "SortList",
	props: {
		items: {
			type: Array,
			default: () => [],
		},
	},
	data: () => ({
		list: [],
		activeBtn: 0,
	}),
	methods: {
		sortById() {
			this.list.sort((a, b) => a.id - b.id);
			this.activeBtn = 0;
		},
		sortByName() {
			this.list.sort((a, b) => a.name.localeCompare(b.name));
			this.activeBtn = 1;
		},
		updateItems() {
			this.list = [...this.items];
		},
	},
	watch: {
		items: {
			handler: function () {
				this.updateItems();
			},
			immediate: true,
		},
	},
};
</script>

<style lang="scss">
.sort-list {
	display: flex;
	flex-flow: column;
	align-items: flex-start;
	justify-content: flex-start;
	width: 50%;
	padding: 20px 10px 0;

	&__header {
		display: flex;
		padding-left: 43px;
		margin-bottom: 20px;

		.btn:last-child {
			margin-left: 100px;
		}
	}

	&__table {
		width: 100%;
		border-collapse: collapse;

		tr:not(:last-child) {
			border-bottom: 1px solid #d9d9d9;
		}

		td {
			padding: 8px;

			&:nth-child(1),
			&:nth-child(2) {
				width: 1px;
				white-space: nowrap;
			}
		}
	}

	&__message {
		padding: 8px 0;
		text-align: center;
		width: 100%;
	}
}
</style>
