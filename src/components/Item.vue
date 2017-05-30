<template>
	<div class="modal fade" id="openItem" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
	  <div class="modal-dialog" role="document">
	    <div class="modal-content">
	      <div class="modal-header">
	        <h5 class="modal-title" id="exampleModalLabel">Brewery: {{brewery.name}}</h5>
	        <button @click.prevent="cleanSelected" type="button" class="close" data-dismiss="modal" aria-label="Close">
	          <span aria-hidden="true">&times;</span>
	        </button>
	      </div>
	      <div class="modal-body">
	        <form>
	          <div class="form-group">
	            <label for="recipient-name" class="form-control-label">Edit Name:</label>
	            <input type="text" class="form-control" id="recipient-name" v-model="brewery.name">
	          </div>
	          <div class="form-group row">
		          <div class="col-md-6">
		          	<label for="recipient-city" class="form-control-label">Edit City:</label>
		            <input type="text" class="form-control" id="recipient-name" v-model="brewery.city">
		          </div>
		          <div class="col-md-6">
		          	<label for="recipient-phone" class="form-control-label">Edit phone:</label>
		            <input type="text" class="form-control" id="recipient-name" v-model="brewery.phone">
		          </div>
	          </div>
	          <div class="form-group">
	            <label for="message-text" class="form-control-label">Edit Description:</label>
	            <textarea class="form-control" id="message-text" v-model="brewery.descript" rows="4"></textarea>
	          </div>
	        </form>
	      </div>
	      <div class="modal-footer">
	        <button @click.prevent="cleanSelected" type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
	        <button @click.prevent="clickSave" type="button" class="btn btn-primary" data-dismiss="modal">Save</button>
	      </div>
	    </div>
	  </div>
	</div>
</template>

<script>
	export default {
		name: 'item',
		props: ['brewery'],
		methods: {
			clickSave(){
				this.$emit('saveBrewery', this.brewery);
			},
			cleanSelected(){
				this.$emit('cleanSelected')
			}
		}
	}	
</script>