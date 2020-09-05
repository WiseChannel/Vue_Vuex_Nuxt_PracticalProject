<template>
  <section class="container">
   <Search />
    <Table />
  </section>
</template>

<script>


import Search from "~/components/Search";
import Table from "~/components/Table";
export default {
  components: {
    Table,
    Search
  }
}
</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

</style>

