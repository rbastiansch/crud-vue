<template>
  <div id="app">
  	<CcHeader @setSearch="searchBreweries"></CcHeader>
  	<div class="row">
  		<CcSidebar></CcSidebar>
  		<CcList :search="search"></CcList>
  	</div>
  </div>
</template>

<script>
import CcHeader from './components/Header.vue';
import CcSidebar from './components/Sidebar.vue';
import CcList from './components/List.vue';

export default {
  name: 'app',
  components: {
  	CcHeader,
  	CcSidebar,
  	CcList
  },
  data(){
  	return {
  		search: '',
  	}
  },
  methods: {
  	searchBreweries(result){
  		this.search = result
  	}
  }
}
</script>
