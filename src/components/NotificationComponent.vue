<template>
<div v-show="loaded" >

  <h2>Notification Details </h2>

  <table>
  <tr>
    <td>Sender Name</td>
    <td>{{item.senderName}}</td>
  </tr>
  <tr>
    <td>Message</td>
    <td>{{item.message}}</td>

  </tr>
  <tr>
    <td>Time Stamp</td>
    <td>{{item.timestamp}}</td>
  </tr>
  
</table>
</div>

</template>

<script>
import { w3cwebsocket } from 'websocket';

const client = new w3cwebsocket('wss://demos.mphalane.co.ls/ws/chat/')

export default {
  name: 'NotificationComponent',
  data() {
    return { 
      notification: Object,
      item: Object,
      loaded: false,
      
    }
  },
  methods: {

 displayNotification(item) {

    navigator.serviceWorker.register('sw.js');

    Notification.requestPermission(function(result) {
    if (result === 'granted') {
      navigator.serviceWorker.ready.then(function(registration) {
        registration.showNotification(item.senderName, {
          title: item.senderName,
          body: item.message,
          icon: 'icon.png',
        });
      });
    }
  });

}

},

created(){
  if (!("Notification" in window)) {
        console.log("This browser does not support desktop notification");
      } else {
        Notification.requestPermission();
      }

  client.onmessage = (message) => {
            const dataFromServer = JSON.parse(JSON.parse(message.data))
            this.loaded = true
            this.item = dataFromServer

            this.displayNotification(dataFromServer)
        }

}

}

</script>

<style scoped>

h2 {
  padding: 14px 20px;
  margin-top: 80px;
  border: none;
}

table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 50%;
  margin: auto;
}

td, th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}
</style>