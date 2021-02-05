<template>
  <CreateForm
    v-if="fields && fields.length > 0"
    :fields="fields"
    redirectUrl="/companies"
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
      fields: null,
      requestUrl: '',
    }
  },
  head() {
    return {
      title: 'Редактирование компании',
    }
  },

  methods: {
    get: async function () {
      try {
        const response = await this.$axios.$get(`/companies/get/${this.$route.params.id}`)
        this.requestUrl = `companies/edit/${this.$route.params.id}`
        this.fields = [
          {
            model: response.company.name,
            key: 'name',
            lable: 'Название',
            type: 'field',
          },
          {
            model: response.company.phone,
            key: 'phone',
            lable: 'Телефон',
            type: 'field',
          },
          {
            model: response.company.email,
            key: 'email',
            lable: 'Email',
            type: 'field',
          },
          {
            model: response.company.description,
            key: 'description',
            lable: 'Заметки',
            type: 'textarea',
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
