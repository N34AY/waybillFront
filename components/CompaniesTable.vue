<template>
  <v-data-table
    :headers="headers"
    :items="items"
    :items-per-page="20"
    :search="search"
    :footer-props="{
      itemsPerPageOptions: [5, 10, 20, 50, 100],
      showFirstLastPage: true,
      'items-per-page-text': 'Записей на странице',
    }"
    class="elevation-2"
  >
    <template v-slot:top>
      <v-row justify="center" align="center">
        <v-col md="10">
          <v-text-field v-model="search" label="Поиск" class="mx-4"></v-text-field>
        </v-col>
        <v-col md="2">
          <v-btn nuxt :to="'/companies/create/'" outlined color="primary">
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
      <v-sheet v-if="item.updated_at">
        {{ new Date(item.updated_at).toLocaleString() }}
      </v-sheet>
    </template>

    <template v-slot:item.actions="{ item }">
      <v-btn nuxt :to="`/companies/edit/${item.id}/`" icon>
        <v-icon large color="blue darken-2"> mdi-pencil-outline </v-icon>
      </v-btn>
      <v-btn @click="remove(item.id)" icon>
        <v-icon large color="red darken-2"> mdi-delete-outline </v-icon>
      </v-btn>
    </template>
  </v-data-table>
</template>


<script>
export default {
  name: 'CompaniesTable',
  props: {
    headers: {
      type: Array,
      required: true,
    },
    items: {
      type: Array,
      required: true,
    },
  },

  data: function data() {
    return {
      search: '',
    }
  },

  methods: {
    remove: async function (id) {
      try {
        await this.$axios.$delete(`/companies/delete/${id}`)
        this.$emit('refresh')
      } catch (error) {
        alert(error)
      }
    }
  }
}
</script>