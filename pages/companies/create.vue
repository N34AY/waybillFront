<template>
  <CreateForm
    :fields="fields"
    redirectUrl="/companies"
    requestUrl="/companies/create"
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
          key: 'phone',
          lable: 'Телефон',
          type: 'field',
        },
        {
          model: null,
          key: 'email',
          lable: 'Email',
          type: 'field',
        },
        {
          model: null,
          key: 'description',
          lable: 'Заметки',
          type: 'textarea',
        },
      ],
    }
  },
  head() {
    return {
      title: 'Создание компании',
    }
  },
}
</script>
