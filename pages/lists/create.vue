<template>
  <CreateForm
    :fields="fields"
    redirectUrl="/lists"
    requestUrl="/lists/create"
    buttonText="Создать"
  />
</template>

<script>
import CreateForm from '~/components/CreateForm.vue'

export default {
  components: {
    CreateForm,
  },

  data: function data() {
    return {
      fields: [
        {
          model: null,
          key: 'name',
          lable: 'Название',
          type: 'field',
        },
        {
          model: null,
          key: 'company',
          lable: 'Компания',
          type: 'select',
          items: [],
        },
      ],
    }
  },
  head() {
    return {
      title: 'Создание списка',
    }
  },

  methods: {
    get: async function () {
      try {
        const items = this.fields[1].items
        const response = await this.$axios.$get('/companies')
        response.companies.forEach(function (company) {
          const obj = {
            name: company.name,
            id: company.id,
          }
          items.push(obj)
        })
      } catch (error) {
        alert(error)
      }
    },
  },

  beforeMount: async function () {
    await this.get()
  },
}
</script>
