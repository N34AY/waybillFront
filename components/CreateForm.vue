<template>
  <v-form @submit.prevent="send">
    <v-sheet v-for="(field, index) in form" :key="index">
      <v-text-field
        v-if="field.type == 'field'"
        v-model="field.model"
        :label="field.lable"
        required
      />

      <v-select
        v-if="field.type == 'select'"
        v-model="field.model"
        :label="field.lable"
        :items="field.items"
        item-text="name"
        item-value="id"
      />

      <v-textarea
        v-if="field.type == 'textarea'"
        v-model="field.model"
        :label="field.lable"
        required
      />
    </v-sheet>

    <v-btn type="submit" outlined color="success">{{ buttonText }}</v-btn>
  </v-form>
</template>

<script>
export default {
  name: 'CreateForm',
  props: {
    fields: {
      type: Array,
      required: true,
    },
    redirectUrl: {
      type: String,
      required: true,
    },
    requestUrl: {
      type: String,
      required: true,
    },
    buttonText: {
      type: String,
      required: true,
    },
  },

  data: function () {
    return {
      form: [],
    }
  },

  methods: {
    send: async function () {
      try {
        const body = {}
        this.form.forEach(function (elem) {
          body[elem.key] = elem.model
        })
        await this.$axios.$post(this.requestUrl, body)
        this.$router.push(this.redirectUrl)
      } catch (error) {
        alert(error)
      }
    },
    formCreator: function (elem) {
      this.form.push({ ...elem })
    },
  },

  beforeMount: function () {
    this.fields.forEach(this.formCreator)
  },
}
</script>
