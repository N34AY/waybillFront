<template>
  <v-data-table
    :headers="headers"
    :items="items"
    :items-per-page="20"
    :search="search"
    show-expand
    :footer-props="{
      itemsPerPageOptions: [5, 10, 20, 50, 100],
      showFirstLastPage: true,
      'items-per-page-text': 'Записей на странице',
    }"
    class="elevation-1 grey lighten-4"
  >
    <template v-slot:top>
      <v-row justify="center" align="center">
        <v-col md="10">
          <v-text-field
            v-model="search"
            label="Поиск"
            class="mx-4"
          ></v-text-field>
        </v-col>
        <v-col md="2">
          <v-btn nuxt :to="'/lists/create/'" outlined color="primary">
            Создать
            <v-icon right color="green darken-2"> mdi-plus-thick </v-icon>
          </v-btn>
        </v-col>
      </v-row>
    </template>

    <template v-slot:item.created_at="{ item }">
      {{ new Date(item.created_at).toLocaleString() }}
    </template>

    <template v-slot:item.updated_at="{ item }">
      <span v-if="item.updated_at">
        {{ new Date(item.updated_at).toLocaleString() }}
      </span>
    </template>

    <template v-slot:item.actions="{ item }">
      <v-btn nuxt :to="`/lists/edit/${item.id}/`" icon>
        <v-icon large color="blue darken-2"> mdi-pencil-outline </v-icon>
      </v-btn>
      <v-btn icon @click="deleteList(item.id)">
        <v-icon large color="red darken-2"> mdi-delete-outline </v-icon>
      </v-btn>
      <v-btn nuxt :to="`/waybills/create/${item.id}/`" icon>
        <v-icon large color="green darken-2"> mdi-plus-thick </v-icon>
      </v-btn>
    </template>

    <template v-slot:expanded-item="{ headers, item }">
      <td :colspan="headers.length" style="padding: 0px" class="white">
        <WaybillsTable :headers="subHeaders" :items="item.waybills" @refresh="$emit('refresh')" class="ml-2 mr-2 mb-2 mt-2"/>
      </td>
    </template>

  </v-data-table>
</template>


<script>
import WaybillsTable from '~/components/WaybillsTable'

export default {
  name: 'ListsTable',
  props: {
    headers: {
      type: Array,
      required: true,
    },
    subHeaders: {
      type: Array,
      required: true,
    },
    items: {
      type: Array,
      required: true,
    },
  },

  components: {
    WaybillsTable,
  },

  data: function data() {
    return {
      search: '',
      subSearch: ''
    }
  },

  methods: {
    deleteList: async function (id) {
      const options = {
        buttonTrueText: 'Удалить',
        buttonFalseText: 'Отмена'
      }
      const result = await this.$confirm('Удалить этот список отчетов?', options)
      if (result) {
        try {
          await this.$axios.$delete(`/lists/delete/${id}`)
          this.$emit('refresh')
        } catch (error) {
          alert(error)
        }
      }
    }
  }
}
</script>