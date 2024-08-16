<template>
    <table border="1" align="center">
        <tr>
          <th v-for="head in gridData.header" v-bind:key="head">{{ head }}</th>
        </tr>
        <tr v-for="row in gridData.rows" v-bind:key="row">
          <td v-for="rows in row" v-bind:key="rows">{{rows}}</td>
        </tr>
    </table>
</template>

<script>
export default {
  name: 'basicGrid',
  props: ['gridData']
}
</script>