<template>
  <nav aria-label="Page navigation example">
    <ul class="pagination">
      <li v-show="showPreviousPage" @click.prevent="firstPage" class="page-item">
        <a class="page-link" href="#" aria-label="Previous">
          <span aria-hidden="true">&laquo;</span>
          <span class="sr-only">Previous</span>
        </a>
      </li>
      <li v-show="showPreviousPage" @click.prevent="previousPage" class="page-item"><a class="page-link" href="#">{{page-1}}</a></li>
      <li @click.prevent="" class="page-item active"><a class="page-link" href="#">{{page}}</a></li>
      <li v-show="showNextPage" @click.prevent="nextPage" class="page-item"><a class="page-link" href="#">{{page+1}}</a></li>
      <li v-show="showNextPage" @click.prevent="lastPage" class="page-item">
        <a class="page-link" href="#" aria-label="Next">
          <span aria-hidden="true">&raquo;</span>
          <span class="sr-only">Next</span>
        </a>
      </li>
    </ul>
  </nav>	
</template>

<script>
export default{
	name: 'pagination',
	props: ['total','page','itensPerPage'],
	computed: {
		totalPages(){
			return Math.ceil(this.total / this.itensPerPage);
		},
		showNextPage(){
			return this.page < this.totalPages;
		},
		showPreviousPage(){
			return this.page > 1;
		}
	},
	methods: {
		nextPage(){
			this.$emit('changePage', this.page + 1);
		},
		previousPage(){
			this.$emit('changePage', this.page - 1);
		},
		firstPage(){
			this.$emit('changePage', 1);
		},
		lastPage(){
			this.$emit('changePage', this.totalPages);
		}
	},

}
</script>