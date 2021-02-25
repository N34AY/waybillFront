<template>
  <v-data-table
    :headers="headers"
    :items="items"
    :items-per-page="20"
    :search="search"
    hide-default-footer
    class="elevation-4"
    dense
  >
    <template v-slot:top>
      <v-text-field v-model="search" label="Поиск" class="mx-4"></v-text-field>
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
      <v-btn nuxt :to="`/waybills/edit/${item.id}/`" icon>
        <v-icon medium color="blue darken-2"> mdi-pencil-outline </v-icon>
      </v-btn>
      <v-btn icon @click="deleteWaybill(item.id)">
        <v-icon medium color="red darken-2"> mdi-delete-outline </v-icon>
      </v-btn>
    </template>
  </v-data-table>
</template>


<script>
export default {
  name: 'WaybillsTable',
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
		deleteWaybill: async function (id) {
      const options = {
        buttonTrueText: 'Удалить',
        buttonFalseText: 'Отмена'
      }
      const result = await this.$confirm('Удалить этот отчет?', options)
      if (result) {
        try {
          await this.$axios.$delete(`/waybills/delete/${id}`)
          this.$emit('refresh')
        } catch (error) {
          alert(error)
        }
      }
    }
	}
}
</script>