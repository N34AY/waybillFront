<template>
  <ListsTable :headers="headers" :subHeaders="subHeaders" :items="items" @refresh="getData" />
</template>

<script>
import ListsTable from '~/components/ListsTable'

export default {
  components: {
    ListsTable,
  },

  data: function data() {
    return {
      headers: [
        {
          text: 'Название',
          align: 'start',
          sortable: true,
          value: 'name',
        },
        {
          text: 'Компания',
          value: 'company.name',
        },
        {
          text: 'Создан',
          value: 'created_at',
        },
        {
          text: 'Изменен',
          value: 'updated_at',
        },
        {
          text: 'Действия',
          value: 'actions',
        },
      ],
      subHeaders: [
        {
          text: 'Название',
          align: 'start',
          sortable: true,
          value: 'name',
        },
        {
          text: 'Создан',
          value: 'created_at',
        },
        {
          text: 'Изменен',
          value: 'updated_at',
        },
        {
          text: 'Действия',
          value: 'actions',
        },
      ],
      items: [],
    }
  },

  head() {
    return {
      title: 'Компании',
    }
  },

  methods: {
    getData: async function () {
      try {
        const response = await this.$axios.$get(`/lists/`)
        this.items = response.lists
      } catch (error) {
        alert(error)
      }
    },
  },

  created() {
    this.getData()
  }
}
</script>
