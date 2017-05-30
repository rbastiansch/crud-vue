<template>
<div class="col-sm-9">
	<CcItem :brewery="selected" @saveBrewery="saveBrewery" @cleanSelected="cleanSelected"></CcItem>
	<CcDelete :brewery="selected" @deleteBrewery="deleteBrewery" @cleanSelected="cleanSelected"></CcDelete>
	<div class="table-responsive">
	<table class="table table-striped">
	  <thead class="thead-inverse">
	    <tr>
	      <th>#</th>
	      <th>Name</th>
	      <th>City</th>
	      <th>Phone</th>
	      <th>Actions</th>
	    </tr>
	  </thead>
	  <tbody>
	    <tr v-for="brewery in breweries">
	      <th scope="row">{{brewery.id}}</th>
	      <td>{{brewery.name}}</td>
	      <td>{{brewery.city}}</td>
	      <td>{{brewery.phone}}</td>
	      <td>
	      	<a @click.prevent="editBrewery(brewery)" href="#" data-toggle="modal" data-target="#openItem">
	      		<i class="fa fa-pencil-square-o" aria-hidden="true"></i>
	      	</a>
	      	<a @click.prevent="editBrewery(brewery)" href="#" data-toggle="modal" data-target="#deleteItem">
	      		<i class="fa fa-trash-o" aria-hidden="true"></i>
	      	</a>
	      </td>
	    </tr>
	  </tbody>
	</table>
	</div>
	<CcPagination :total="total" :page="page" :itensPerPage="itensPerPage" @changePage="onChangePage" class="row justify-content-center"></CcPagination>
</div>	
</template>

<script>
import CcPagination from './Pagination.vue';
import CcItem from './Item.vue';
import CcDelete from './Delete.vue';
export default{
	name: 'list',
	props: ['search'],
	components: {
		CcPagination,
		CcItem,
		CcDelete
	},
	data(){
		return {
			breweries: [],
			itensPerPage: 10,
			page: 1,
			total: 0,
			selected: {},
		}
	},
	watch: {
		search: function(){
			this.loadBreweries();
		}
	},
	methods: {
		onChangePage(page){
			this.page = page;
			this.loadBreweries();
		},
		loadBreweries(){
			const t = this;

			let startList = (this.page * this.itensPerPage) - this.itensPerPage;
			let endList = this.page * this.itensPerPage;
			let searchString = '';

			if(this.search){
				searchString = `&name_like=${this.search}`
			}

			this.$http.get(`/breweries?_start=${startList}&_end=${endList}${searchString}`).then(response => {
				t.breweries = response.body;
				t.total = parseInt(response.headers.map['X-Total-Count']);
			}, response => {
				console.error(error)
			});
		},
		editBrewery(brewery){
			this.selected = brewery;
		},
		saveBrewery(){
			if(this.selected.id != null){
				this.$http.put(`/breweries/${this.selected.id}`, this.selected).then(response => {
					this.$set(this, 'selected', {})
				}, error => {
					console.error(error)
				})
			}else{
				this.$http.post('/breweries/', this.selected).then(response => {
					this.$set(this, 'selected', {})
				}, error => {
					console.error(error)
				})
			}
			this.selected = {};
		},
		deleteBrewery(){
			this.$http.delete(`/breweries/${this.selected.id}`).then(result => {
				this.cleanSelected();
			})
		},
		searchResult(){
			this.loadBreweries();
		},
		cleanSelected(){
			this.selected = {};
			this.loadBreweries();
		}
	},
	created(){
		this.loadBreweries();

	}
}
</script>