<template>
	<div id="app">
		<div class="container">
			<SortList :items="uncheckedItems" />
			<SortList :items="checkedItems" />
		</div>
	</div>
</template>

<script>
import facultiesArr from "@/assets/js/faculties";
import SortList from "@/components/SortList";

export default {
	name: "App",
	components: { SortList },
	data: () => ({
		faculties: [],
	}),
	computed: {
		checkedItems() {
			return this.faculties.filter((el) => el.checked);
		},
		uncheckedItems() {
			return this.faculties.filter((el) => !el.checked);
		},
	},
	created() {
		this.faculties = JSON.parse(JSON.stringify(facultiesArr))
			.map(({ data }) => data)
			.map(({ id, name, headOfDepartment }) => ({
				id,
				name,
				headOfDepartment,
				checked: false,
			}));
	},
};
</script>

<style lang="scss">
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	color: #2c3e50;
}
</style>
