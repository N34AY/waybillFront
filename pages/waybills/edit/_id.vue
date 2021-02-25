<template>
  <div>
    <v-sheet v-if="sheet">
      <ExcelEditor :columns="columns" :sheet="sheet" />
    </v-sheet>
    <v-form @submit.prevent="send">
      <v-text-field v-model="name" label="Название" required />

      <v-select
        v-model="lst"
        label="Список"
        :items="lists"
        item-text="name"
        item-value="id"
      />

      <v-btn type="submit" outlined color="success">Сохранить</v-btn>
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
      sheet: null,
    }
  },
  head() {
    return {
      title: 'Редактирование накладной',
    }
  },

  methods: {
    get: async function () {
      try {
        const listsResponse = await this.$axios.$get('/lists')
				this.lists = listsResponse.lists
				
				const waybillResponse = await this.$axios.$get(`/waybills/get/${this.$route.params.id}`)
				this.sheet = waybillResponse.waybill.sheet
				this.name = waybillResponse.waybill.name
				this.lst = waybillResponse.waybill.lst
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
        await this.$axios.$post(`/waybills/edit/${this.$route.params.id}`, body)
        this.$router.push('/lists/')
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
