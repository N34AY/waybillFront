<template>
  <v-row justify="center" align="center">
    <v-col>
      <Dashboard :cards="cards" />
    </v-col>
    <v-col>
      <v-card>
        <v-card-title class="headline"> Панель управления </v-card-title>
        <v-card-text>
          <p>
            Панель управления накладными и их учета.
          </p>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import Dashboard from '~/components/Dashboard.vue'

export default {
  components: {
    Dashboard,
  },

  data: function data() {
    return {
      cards: [
        {
          title: 'Компании',
          color: 'deep-purple darken-1',
          icon: 'mdi-account-group-outline',
          link: '/companies',
          flex: 12,
        },
        {
          title: 'Накладные',
          color: 'cyan darken-1',
          icon: 'mdi-file-table-outline',
          link: '/lists',
          flex: 6,
        },
        {
          title: 'Статистика',
          color: 'green darken-1',
          icon: 'mdi-sort-clock-descending-outline',
          link: '/statistics',
          flex: 6,
        },
      ],
    }
  },
}
</script>
