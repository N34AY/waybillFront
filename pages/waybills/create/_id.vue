<template>
  <div>
    <ExcelEditor :columns="columns" :sheet="sheet" />
    <v-form @submit.prevent="send">
      <v-text-field v-model="name" label="Название" required />

      <v-select
        v-model="lst"
        label="Список"
        :items="lists"
        item-text="name"
        item-value="id"
      />

      <v-btn type="submit" outlined color="success">Создать</v-btn>
    </v-form>
  </div>
</template>

<script>
import ExcelEditor from '~/components/ExcelEditor.vue'

export default {
  components: {
    ExcelEditor,
  },

  data: function data() {
    return {
      name: '',
      lst: '',
      lists: [],
      columns: [
        {
          name: 'Артикул',
          data: 'article',
        },
        {
          name: 'Название',
          data: 'name',
        },
        {
          name: 'Стоимость',
          data: 'price',
        },
        {
          name: 'Кол-во',
          data: 'quantity',
        },
        {
          name: 'Сумма',
          data: 'sum',
        },
      ],
      sheet: [{}, {}, {}, {}, {}, {}, {}, {}, {}, {}],
    }
  },
  head() {
    return {
      title: 'Создание накладной',
    }
  },

  methods: {
    get: async function () {
      try {
        const response = await this.$axios.$get('/lists/')
        this.lists = response.lists
      } catch (error) {
        alert(error)
      }
    },

    getList: async function () {
      try {
        const response = await this.$axios.$get(`/lists/get/${this.$route.params.id}`)
        this.lst = response.list
      } catch (error) {
        alert(error)
      }
    },

    send: async function () {
      try {
        const body = {
          name: this.name,
          lst: this.lst.id,
          sheet: this.sheet,
        }
        await this.$axios.$post('/waybills/create', body)
        this.$router.push('/lists/')
      } catch (error) {
        alert(error)
      }
    },
  },

  beforeMount: async function () {
    await this.get()
		await this.getList()
  },
}
</script>
