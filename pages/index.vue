<template>
  <b-container>
        <b-row >
            <b-col>
              <b-card :img-src="weatherItem.image"
              overlay>
                <b-card-header block>
                  <b-card-title>{{ weatherItem.city }}の天気</b-card-title>
                </b-card-header>
                <b-card-body>
                  <b-img :src="weatherItem.icon"></b-img>
                <b-card-sub-title class="p-3 bg-info text-white">{{ weatherItem.weather }}</b-card-sub-title>
                  <b-card-text>
                    <p>現在の気温:　{{ weatherItem.maxTemp }}℃</p>
                  </b-card-text>
                </b-card-body>
              </b-card>
            </b-col>
        </b-row>
  </b-container>
</template>

<script>
import cloudsImage from '@/static/pr00153-640x480.jpg'
export default {
  data: () => ({  
    qiitaData: [],
    homeTitle: '',
    oWobj: {},
    weatherItem: {
      city: '',
      image: '',
      weather: '',
      maxTemp: 0,
      minTemp: 0
    }

  }),

  async created() {
    this.homeTitle = 'MIURA PAGE'
    const apiKey = "5f75aaa751fc6d370dbd9c2744a0e75f"
    const city = 'Utsunomiya'
    const iconPass = 'http://openweathermap.org/img/w/'

    this.oWobj = await this.$axios.$get('http://api.openweathermap.org/data/2.5/forecast?q=' + city + ',jp&units=metric&lang=ja&APPID=' + apiKey)
    this.weatherItem.city = this.oWobj.city.name
    
    this.weatherItem.icon = iconPass + this.oWobj.list[5].weather[0].icon + '.png'
    this.weatherItem.weather = this.oWobj.list[3].weather[0].description
    this.weatherItem.minTemp = this.oWobj.list[3].main.temp_min
    this.weatherItem.maxTemp = this.oWobj.list[3].main.temp_max
    let imagePass
    console.log(parseInt(this.oWobj.list[3].weather[0].id))
    switch (Math.floor(this.oWobj.list[3].weather[0].id / 100)) {
      case (8):
        imagePass = cloudsImage
        break;
    
      default:
        imagePass = '失敗'
        break;
    }
    this.weatherItem.image = imagePass

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

