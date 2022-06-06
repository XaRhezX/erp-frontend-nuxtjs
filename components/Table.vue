<template>
  <div class="table-responsive</div>">
    <table id="tableComponent" class="table table-bordered table-hover">
      <thead>
        <tr>
          <!-- loop through each value of the fields to get the table header -->
          <th v-for="field in response.fields" :key='field' @click="sortTable(field)">
            {{ field }} <i class="bi bi-sort-alpha-down" aria-label='Sort Icon'></i>
          </th>
        </tr>
      </thead>
      <tbody>
        <!-- Loop through the list get the each student data -->
        <tr v-for="item in response.data" :key='item.id'>
          <td v-for="field in response.fields" :key='field'>{{ item[field] }}</td>
        </tr>
      </tbody>
      <tfoot v-if="response.links.length" class="w-100">
        <ul class="pagination">
          <li v-for="paginate, index  in response.links" :key="index" class="page-item"
            :class="paginate.active == true ? 'active' : ''" @click="handlePageChange(paginate.url)">
            <button v-if="index == 0" class="page-link" href="#" tabindex="-1" aria-disabled="true"
              :disabled="paginate.url == null">
              <chevron-left-icon />
              Previous
            </button>
            <button v-else-if="index == response.links.length - 1" class="page-link" href="#" aria-disabled="true"
              :disabled="paginate.url == null">
              Next
            </button>
            <button v-else class="page-link" :disabled="paginate.url == null">
              {{ paginate.label }}
            </button>
          </li>
        </ul>
      </tfoot>
    </table>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  name: 'TableComponent',
  props: {
    response: {
      type: Object,
    }
  },
  methods: {
    async handlePageChange(url) {
      console.log(url)
      let paginate = [];
      paginate = await this.$axios.$get(url);
      paginate.fields = this.response.fields;
      this.response = paginate;
    }
  }
}
</script>
