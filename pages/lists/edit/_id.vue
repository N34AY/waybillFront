<template>
  <CreateForm
    v-if="fields && fields.length > 0"
    :fields="fields"
    redirectUrl="/lists"
    :requestUrl="requestUrl"
    buttonText="Сохранить"
  />
</template>

<script>
import CreateForm from '~/components/CreateForm.vue'

export default {
  components: {
    CreateForm,
  },

  data: function () {
    return {
      fields: [],
      requestUrl: '',
    }
  },
  head() {
    return {
      title: 'Редактирование списка',
    }
  },

  methods: {
    get: async function () {
      try {
        const listResponse = await this.$axios.$get(`/lists/get/${this.$route.params.id}`)
        const companiesResponse = await this.$axios.$get('companies')

        const items = []
        companiesResponse.companies.forEach(function (company) {
          const obj = {
            name: company.name,
            id: company.id,
          }
          items.push(obj)
        })

        this.requestUrl = `lists/edit/${this.$route.params.id}`
        this.fields = [
          {
            model: listResponse.list.name,
            key: 'name',
            lable: 'Название',
            type: 'field',
          },
          {
            model: listResponse.list.company,
            key: 'company',
            lable: 'Компания',
            type: 'select',
            items: items,
          },
        ]
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
