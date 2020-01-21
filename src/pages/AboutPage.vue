<template>
  <q-page class="flex full-width">
    <div class="q-ma-lg">
      <h1 class="text-h3">{{title}}</h1>
      <div v-for="(value, name) in responseData" :key="name">
        <h2 class="text-h6">{{name.toUpperCase()}}</h2>
        <p>{{value}}</p>
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'AboutPage',
  data () {
    return {
      title: 'About',
      responseData: {}
    }
  },
  created () {
    this.getAboutData()
  },
  methods: {
    async getAboutData () {
      try {
        let response = await this.$axios.get(this.$apiurl + '/about/')
        let data = await response.data
        this.responseData = data
      } catch (error) {
        console.log(error)
      }
    }
  }
}
</script>
