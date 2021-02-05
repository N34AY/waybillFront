<template>
  <DataTable
    :headers="headers"
    addButtonText="Добавить компанию"
    basePath="companies"
    :dataOrder="dataOrder"
    object="companies"
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
      headers: [
        'Название',
        'Телефон',
        'Почта',
        'Описание',
        'Создана',
        'Изменена',
      ],
      dataOrder: [
        'name',
        'phone',
        'email',
        'description',
        'created_at',
        'updated_at',
      ],
    }
  },
  head() {
    return {
      title: 'Компании',
    }
  },
}
</script>
