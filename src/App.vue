<template>
  <div>
    <slot :list="paginatedList" :pages="pagination.pages"></slot>
    <slot name="linksWrapper" :list="paginatedList" :pages="pagination.pages">
      <div class="pagination-wrapper" v-if="pagination.pages.length > 1">
        <ul class="pagination mg-b-0">
          <li class="page-item" v-if="pagination.page != 1" @click="pagination.page--">
            <a class="page-link" href="#" aria-label="Previous">
              <i class="icon ion-ios-arrow-left"></i>
            </a>
          </li>
          <li
            class="page-item"
            :class="{'active': (pagination.page == pageNumber)}"
            v-for="pageNumber in pages.slice(pagination.page-1, pagination.page+5)"
            @click="pagination.page = pageNumber"
            :key="pageNumber"
          >
            <a class="page-link" href="#" v-text="pageNumber"></a>
          </li>
          <li
            class="page-item hidden-xs-down"
            @click="pagination.page++"
            v-if="pagination.page < pagination.pages.length"
          >
            <a class="page-link" href="#" aria-label="Last">
              <i class="icon ion-ios-arrow-right"></i>
            </a>
          </li>
        </ul>
      </div>
    </slot>
  </div>
</template>

<script>
export default {
  computed: {
    paginatedList() {
      if (!this.list || !this.perPage) return [];

      let numberOfPages = Math.ceil(this.list.length / this.perPage);
      this.pagination.pages = [];
      for (let index = 1; index <= numberOfPages; index++) {
        this.pagination.pages.push(index);
      }
      let from = this.pagination.page * this.perPage - this.perPage;
      let to = this.pagination.page * this.perPage;
      return this.list.slice(from, to);
    }
  },
  data: () => ({
    pagination: {
      page: 1,
      pages: []
    }
  }),
  props: ["list", "perPage"]
};
</script>