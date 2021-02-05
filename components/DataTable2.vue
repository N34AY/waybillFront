<template>
  <v-data-table
    :headers="headers"
    :items="items"
    :items-per-page="20"
		:search="search"
    class="elevation-1"
  ></v-data-table>
</template>


<script>
export default {
  name: 'DataTable2',
  props: {
    headers: {
      type: Array,
      required: true,
    },
    items: {
      type: Array,
      required: true,
		},
  },
}
</script>