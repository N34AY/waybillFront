<template>
  <DataTable
    :headers="headers"
    addButtonText="Добавить накладную"
    basePath="waybills"
    :dataOrder="dataOrder"
    object="waybills"
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
      headers: ['Название', 'Список', 'Создана', 'Изменена'],
      dataOrder: ['name', 'lst', 'created_at', 'updated_at'],
    }
  },
  head() {
    return {
      title: 'Накладные',
    }
  },
}
</script>
