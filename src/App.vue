<template>
  <div id="app">
    <div class="container">
      <div class="columns">
        <div class="column is-3">
          <div class="section">
            <aside class="menu">
              <p class="menu-label">
                MQTT-CONNECTOR/PAO/#
              </p>
              <ul class="menu-list">
                <li><a>DEMO 1</a></li>
                <li><a>DEMO 2</a></li>
              </ul>
            </aside>
          </div>
        </div>
        <div class="column">

        </div>
      </div>
    </div>

  </div>
</template>

<script>
  import 'bulma/css/bulma.min.css'
  import mqtt from 'mqtt'

  let mqtt_config = {
    host: 'mqtt.cmmc.io',
    username: '',
    password: '',
    sub: 'MQTT-CONNECTOR/PAO/#',
    options: {
      clientId: 'CMMC_' + Math.random().toString(16).substr(2, 8),
      clean: true,
      port: 9001
    }
  }

  let client = mqtt.connect('mqtt://' + mqtt_config.host, mqtt_config.options)

  client.on('connect', function () {
    client.subscribe(mqtt_config.sub)
  })

  client.on('message', function (topic, message, packet) {
    //console.log(message.toString())
    try {
      let messageIncome = JSON.parse(message.toString())
      console.log(messageIncome)
    } catch (e) {

    }
  })

  export default {
    name: 'App',
    components: {}
  }

</script>

<style>
  #app {
    font-family: 'Gothic A1', sans-serif;
    /*font-family: 'Avenir', Helvetica, Arial, sans-serif;*/
    /*-webkit-font-smoothing: antialiased;*/
    /*-moz-osx-font-smoothing: grayscale;*/
    /*text-align: center;*/
    /*color: #2c3e50;*/
    /*margin-top: 60px;*/
  }
</style>
