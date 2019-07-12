<template>
  <div>
    <a :href="url1">{{url1}}</a>
    <el-switch
      v-model="isListening1"
      active-color="#13ce66"
      inactive-color="#ff4949">
    </el-switch>

    <br/>

    <a :href="url2">{{url2}}</a>
    <el-switch
      v-model="isListening2"
      active-color="#13ce66"
      inactive-color="#ff4949">
    </el-switch>

    <br/>
    <a :href="url3">{{url3}}</a>
    <el-switch
      v-model="isListening3"
      active-color="#13ce66"
      inactive-color="#ff4949">
    </el-switch>
  </div>
</template>

<script>

import axios from 'axios'
import qs from 'qs'

export default {

  watch: {
    isListening1(newValue) {
      axios.post('http://localhost:3000/api/status', qs.stringify({"URL":this.url1, "status":newValue}));
    },
    isListening2(newValue) {
      axios.post('http://localhost:3000/api/status', qs.stringify({"URL":this.url2, "status":newValue}));
    },
    isListening3(newValue) {
      axios.post('http://localhost:3000/api/status', qs.stringify({"URL":this.url3, "status":newValue}));
    }
  },

  async asyncData(context) {
    let { data } = await axios.get('http://localhost:3000/api/status')
    return { 
      url1: data[0].url,
      isListening1: data[0].listening,
      url2: data[1].url,
      isListening2: data[1].listening,
      url3: data[2].url,
      isListening3: data[2].listening,
    }
  }
}
</script>
