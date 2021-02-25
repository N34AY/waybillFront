<template>
  <v-sheet class="mb-10">
    <hot-table :settings="settings" :data="sheet">
      <hot-column
        v-for="(column, index) in columns"
        :key="index"
        :title="column.name"
        :data="column.data"
      />
    </hot-table>
  </v-sheet>
</template>

<script>
import { HotTable, HotColumn } from '@handsontable/vue'
import Handsontable from 'handsontable'

export default {
  name: 'ExcelEditor',
  props: {
    columns: {
      type: Array,
      required: true,
    },
    sheet: {
      type: Array,
      required: true,
    },
  },

  components: {
    HotTable,
    HotColumn,
  },

  data: function () {
    return {
      settings: {
        rowHeaders: true,
        columnSorting: true,
        stretchH: 'all',
        manualColumnResize: true,
        manualRowResize: true,
        manualColumnMove: true,
        manualRowMove: true,
        formulas: true,
        contextMenu: {
          items: {
            row_above: {
              name: 'Добавить строку выше',
            },
            row_below: {
              name: 'Добавить строку ниже',
            },
            separator: Handsontable.plugins.ContextMenu.SEPARATOR,
            clear_custom: {
              name: 'Очистить таблицу',
              callback: function () {
                this.clear()
              },
            },
          },
        },
        licenseKey: 'non-commercial-and-evaluation',
      },
    }
  },

  methods: {
    calculate: function () {

    },
  },
}
</script>

<style src="../node_modules/handsontable/dist/handsontable.full.css"></style>
