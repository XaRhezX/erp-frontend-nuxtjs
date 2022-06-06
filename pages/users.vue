<template>
  <div class="container-xl">
    <div class="page-header d-print-none">
      <div class="row g-2 align-items-center">
        <div class="col">
          <!-- Page pre-title -->
          <div class="page-pretitle">
            User Settings
          </div>
          <h2 class="page-title">
            Account
          </h2>
        </div>
        <!-- Page title actions -->
        <div class="col-12 col-md-auto ms-auto d-print-none">
          <div class="btn-list">
            <a href="#" class="btn btn-primary d-none d-sm-inline-block" data-bs-toggle="modal"
              data-bs-target="#modal-report">
              <plus-icon />
              Add New Account
            </a>
            <a href="#" class="btn btn-primary d-sm-none btn-icon" data-bs-toggle="modal" data-bs-target="#modal-report"
              aria-label="Create new report">
              <plus-icon />
            </a>
          </div>
        </div>

        <Table :response='response'></Table>
      </div>
    </div>
  </div>
</template>

<script>
import Table from '~/components/Table.vue'
export default {
  components: { Table },
  middleware: 'auth',
  data() {
    return [];
  },
  async asyncData({ $axios }) {
    let response = [];
    response = await $axios.$get("user");
    response.fields = [
      'name', 'email', 'created_at'
    ];
    return { response: response };
  }
}
</script>
