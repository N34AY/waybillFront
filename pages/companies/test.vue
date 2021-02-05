<template>
  <DataTable2
    :headers="headers"
		:items="items"
  />
</template>

<script>
import DataTable2 from '~/components/DataTable2.vue'

export default {
  components: {
    DataTable2,
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
          value: 'company',
        },
        {
          text: 'Создан',
          value: 'created_at',
        },
        {
          text: 'Изменен',
          value: 'updated_at',
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
        const response = await this.$axios.$get(`/lists`)
        this.items = response.lists
      } catch (error) {
        alert(error)
      }
    },
  },

  created() {
    this.getData()
  },
}
</script>
