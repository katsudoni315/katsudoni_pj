<template>
  <section class="container">
    <b-card class="main-card">
      <b-card-title>{{ homeTitle }}</b-card-title>
      <b-card-body>
        千里の道も一歩より
      </b-card-body>
    </b-card>
  </section>
</template>

<script>
export default {
  data: () => ({  
    qiitaData: Array,
    homeTitle: String,

  }),

  async mounted() {
    
  },

  async created (){
    this.homeTitle = 'MIURA PAGE'
    this.qiitaData = JSON.stringify(await this.$axios.$get('https://qiita.com/api/v2/items?query=tag:nuxt.js'),true, '')
  }
}
</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

.main-card {
  width: 100%;
  height: 100%;
}
</style>

