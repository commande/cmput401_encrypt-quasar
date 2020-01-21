<template>
  <q-page class="flex full-width">
    <div class="q-ma-lg">
      <h1 class="text-h3">{{title}}</h1>
      <div class="overflow-hidden" v-for="(item, index) in responseData" :key="index">
        <p v-for="(value, name, index) in item" :key="index">
          <b>{{name.toUpperCase()}}:</b> {{value}}
        </p>
        <hr class="q-mb-lg">
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'HistoryPage',
  data () {
    return {
      title: 'History',
      responseData: {}
    }
  },
  created () {
    this.getHistoryData()
  },
  methods: {
    async getHistoryData () {
      try {
        let response = await this.$axios.get(this.$apiurl + '/history/')
        let data = await response.data
        this.responseData = data
      } catch (error) {
        console.log(error)
      }
    }
  }
}
</script>
