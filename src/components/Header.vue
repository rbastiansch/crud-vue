<template>
	<nav class="navbar navbar-toggleable-md navbar-inverse bg-inverse mb-1">
	  <a class="navbar-brand" href="#">Vue Application</a>
	  <button type="button" class="btn btn-success mr-sm-2" data-toggle="modal" data-target="#openItem">Create new item</button>
	  	<form class="form-inline">
		    <input class="form-control mr-sm-2" type="text" placeholder="Search" v-model="search">
		    <button @click.prevent="searchBreweries" class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
		</form>

	</nav>
</template>

<script>
export default{
	name: 'header',
	data(){
		return {
			search: ''
		}
	},
	watch: {
		search: function(){
			this.searchBreweries();
		}
	},
	methods: {
		searchBreweries(){
			this.$emit('setSearch', this.search)
		}
	}
}
</script>