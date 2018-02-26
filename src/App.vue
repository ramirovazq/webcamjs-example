<template>
  <div id="app">
    <h2>Webcam maestro</h2> 
    <div v-show="camera_enable">
        <div id="my_camera" style="width:320px; height:240px;"></div>
    </div>


    <div v-if="camera_enable">
        <button @click.prevent="inhabilita_camara">inhabilita  camara</button>
        <button @click.prevent="take_snapshot">guardar foto</button>
    </div>
    <div v-else>
        <button @click.prevent="habilita_camara">habilita  camara</button>
    </div>

    <hr/>
    <img :src="photo"></img>
    <hr/>
  </div>
</template>

<script>
import Webcam from 'webcamjs'
export default {
  name: 'app',
  data () {
    return {
      camera_enable: true,
      photo: null
    }
  },
  methods: {
    habilita_camara(){
        console.log('camara habilitada ----------------');
        this.camera_enable = true;
        Webcam.attach('#my_camera');
    },
    inhabilita_camara(){
        this.camera_enable = false;
        console.log('camara inhabilitada ----------------');
        Webcam.reset();
    },
    take_snapshot(){
      Webcam.snap((data_uri) => {
        this.photo = data_uri;
        /* document.getElementById('my_result').innerHTML = '<img src="'+data_uri+'"/>'; */
      });
      this.inhabilita_camara();
    } 
  }, // methods
  mounted () {
    this.habilita_camara();
  } // mounted
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
