<template>
	<div class="modal fade" id="deleteItem" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
	  <div class="modal-dialog" role="document">
	    <div class="modal-content">
	      <div class="modal-header">
	        <h5 class="modal-title" id="exampleModalLabel">Delete {{brewery.name}}</h5>
	        <button @click.prevent="cleanSelected" type="button" class="close" data-dismiss="modal" aria-label="Close">
	          <span aria-hidden="true">&times;</span>
	        </button>
	      </div>
	      <div class="modal-body">
	        <p>Do you really want to delete {{brewery.name}}</p>
	      </div>
	      <div class="modal-footer">
	        <button @click.prevent="cleanSelected" type="button" class="btn btn-secondary" data-dismiss="modal">No, I don't!</button>
	        <button @click.prevent="clickDelete" type="button" class="btn btn-danger" data-dismiss="modal">Yes, I want to delete it!</button>
	      </div>
	    </div>
	  </div>
	</div>	
</template>

<script>
	export default {
		name: 'delete',
		props: ['brewery'],
		methods: {
			clickDelete(){
				this.$emit('deleteBrewery', this.brewery);
			},
			cleanSelected(){
				this.$emit('cleanSelected')
			}
		}
	}
	
</script>