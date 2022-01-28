<template>
	<div class="container m-5 p-2 rounded mx-auto shadow">
		<!-- App title section -->
		<div class="row m-1 p-4">
			<div class="col-12 col-md-12">
				<div class="p-1 h1 text-primary text-center mx-auto display-inline-block">
					<u>My Todo-s</u>
				</div>
				<add-form-component v-on:reloadlist="getList()"></add-form-component>
				<div class="col-auto p-2 float-right">
					<label class="">Sort</label>
					<button v-on:click="ascending =!ascending" class="sort-button">
						<i v-if="ascending" class="fa fa fa-sort-amount-asc text-success"></i>
						<i v-else class="fa fa fa-sort-amount-desc text-success"></i>
    				</button>
				</div>
				<br>
				<list-view-component :items="sortTasks" v-on:reloadlist="getList()">
				</list-view-component>
				<span class="p-1">
                    <h6>{{ itemLefts.length }}/{{ items.length }} item left</h6>
                </span>
			</div>
		</div>
	</div>
</template>

<script>
import AddFormComponent from './AddFormComponent';
import ListViewComponent from './ListViewComponent';

export default {
	components: {
		AddFormComponent,
		ListViewComponent,
	},
	data: function () {
		return {
			items: [],
			ascending: true,
		};
	},
	methods: {
		getList() {
			axios
				.get('api/items', {})
				.then((response) => {
					this.items = response.data;
				})
				.catch((error) => {
					console.log(error);
				});
		},
	},
	created() {
		this.getList();
	},
	computed: {
		itemLefts() {
			return this.items.filter((t) => !t.completed);
		},
		sortTasks(){
			if (!this.ascending) {
				return this.items.reverse();
			}
			return this.items;
		},
	},
};
</script>
<style>
body {
	background: #f8f8f8;
	font-family: 'Open Sans', sans-serif;
	line-height: 1.6;
}
.sort-button {
	background-color: rgba(0,0,0,0);
	border: none;
	height: 100%;
}
</style>
