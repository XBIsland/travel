<template>
  <div>
    <city-header></city-header>
    <city-search :cities="cities" @handleFocus="handleFocus"
      @handleBlur="handleBlur"
    ></city-search>
    <city-list
      :cities="cities"
      :hot="hotCities"
      :letter="letter"
    ></city-list>
    <city-alphabet
      :cities="cities"
      @change="hangleLetterChange"
      :showAlp = "showAlp"
    ></city-alphabet>
  </div>
</template>

<script>
import axios from 'axios'
import CityHeader from './components/header'
import CitySearch from './components/search'
import CityList from './components/list'
import CityAlphabet from './components/alphabet'
export default {
  name: 'City',
  components: {
    CityHeader,
    CitySearch,
    CityList,
    CityAlphabet
  },
  data () {
    return {
      cities: {},
      hotCities: [],
      letter: '',
      showAlp: true
    }
  },
  methods: {
    getCityInfo () {
      axios.get('/api/city.json').then(this.handleGetCityInfoSucc)
    },
    handleGetCityInfoSucc (res) {
      res = res.data
      if (res.ret && res.data) {
        const data = res.data
        this.cities = data.cities
        this.hotCities = data.hotCities
      }
    },
    hangleLetterChange (letter) {
      this.letter = letter
    },
    handleFocus () {
      this.showAlp = false
    },
    handleBlur () {
      this.showAlp = true
    }
  },
  mounted () {
    this.getCityInfo()
  }
}
</script>

<style lang="stylus" scoped>

</style>
