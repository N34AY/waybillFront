<template>
  <CompaniesTable :headers="headers" :items="items"  @refresh="getData"/>
</template>

<script>
import CompaniesTable from '~/components/CompaniesTable'

export default {
  components: {
    CompaniesTable,
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
          text: 'Телефон',
          value: 'phone',
        },
        {
          text: 'Email',
          value: 'email',
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
        const response = await this.$axios.$get(`/companies/`)
        this.items = response.companies
      } catch (error) {
        alert(error)
      }
    }
  },

  created() {
    this.getData()
  }
}
</script>
