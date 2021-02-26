<template>
  <v-card class="mx-auto" max-width="500">
    <v-container fluid>
      <v-row dense justify="center" align="center">
        <v-col v-for="card in cards" :key="card.title" :cols="card.flex">
          <v-card :to="card.link" :color="card.color" dark height="200px">
            <v-card-title v-text="card.title"></v-card-title>
						<v-card-text>
							<v-icon x-large>{{ card.icon }}</v-icon>
						</v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-card>
</template>


<script>
export default {
  name: 'Dashboard',
  props: {
    cards: {
      type: Array,
      required: true,
    }
  },

  data: function data() {
    return {
    }
  },

  methods: {},
}
</script>