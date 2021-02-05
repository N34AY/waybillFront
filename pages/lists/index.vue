<template>
  <DataTable
    :headers="headers"
    addButtonText="Добавить список"
    basePath="lists"
    :dataOrder="dataOrder"
    object="lists"
  />
</template>

<script>
import DataTable from '~/components/DataTable.vue'

export default {
  components: {
    DataTable,
  },

  data: function data() {
    return {
      headers: ['Название', 'Компания', 'Создан', 'Изменен'],
      dataOrder: ['name', 'company', 'created_at', 'updated_at'],
    }
  },
  head() {
    return {
      title: 'Компании',
    }
  },
}
</script>
