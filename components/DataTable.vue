<template>
  <v-simple-table fixed-header>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left" v-for="item in headers" :key="item.message">
            {{ item }}
          </th>
          <th>
            <v-btn nuxt :to="`/${basePath}/create`" outlined color="primary">
              {{ addButtonText }}
              <v-icon right color="green darken-2"> mdi-plus-thick </v-icon>
            </v-btn>
          </th>
        </tr>
      </thead>
      <tbody>
        <v-sheet v-if="data.length == 0">
          <v-skeleton-loader
            type="list-item-two-line"
          ></v-skeleton-loader>
        </v-sheet>
        <tr v-for="(item, index) in data" :key="index">
          <td v-for="(key, index) in dataOrder" :key="index">
            {{ item[key] }}
          </td>
          <td>
            <v-btn nuxt :to="`/${basePath}/edit/${item.id}`" icon>
              <v-icon large color="blue darken-2"> mdi-pencil-outline </v-icon>
            </v-btn>
            <v-btn @click="remove(item.id)" icon>
              <v-icon large color="red darken-2"> mdi-delete-outline </v-icon>
            </v-btn>
          </td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
</template>

<script>
export default {
  name: 'DataTable',
  props: {
    headers: {
      type: Array,
      required: true,
    },
    object: {
      type: String,
      required: true,
    },
    dataOrder: {
      type: Array,
      required: true,
    },
    addButtonText: {
      type: String,
      required: true,
    },
    basePath: {
      type: String,
      required: true,
    },
  },

  data: function data() {
    return {
      data: [],
    }
  },

  methods: {
    getData: async function () {
      try {
        const response = await this.$axios.$get(`/${this.basePath}`)
        this.data = response[this.object]
      } catch (error) {
        alert(error)
      }
    },

    remove: async function (id) {
      try {
        await this.$axios.$delete(`/${this.basePath}/delete/${id}`)
        this.getData()
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
