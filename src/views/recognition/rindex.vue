<template>
    <div class="containerr">
      <div class="row">
        <div class="col-lg-8 offset-lg-2">
          <form v-on:submit.prevent="Supmit">
            <div class="form-group">
                <div class="field">
                      <input type="number" class="input" placeholder="Identifier" v-model="Identifier" >
                </div>
              </div>
            <button type="submit" value = 'Capture' class="btn btn-light">Capture</button>
          </form>
          <div class="video-container">
            <video ref="video" autoplay></video>
          </div>
          <h1>{{}}</h1>
        </div>
        <button class="backbutton" onclick="history.back()"> Back</button>
      </div>
    </div>
</template>

 

<script>
import axios from 'axios';

  export default {
    data() {
      return {
        video: null,
        stream: null,
        Identifier: null
      };
    },
    mounted() {
      this.video = this.$refs.video;
      navigator.mediaDevices.getUserMedia({ video: true }).then((stream) => {
        this.video.srcObject = stream;
        this.stream = stream;
        this.startStreaming(stream);
      });
    },
    beforeDestroy() {
      if (this.stream) {
        const tracks = this.stream.getTracks();
        tracks.forEach((track) => {
          track.stop();
        });
      }
    },
    methods: {
      startStreaming(stream) {
        const canvas = document.createElement('canvas');
        const context = canvas.getContext('2d');
        const fps = 30;
        setInterval(() => {
          context.drawImage(this.video, 0, 0, canvas.width, canvas.height);
          const dataURL = canvas.toDataURL('image/jpeg', 0.5);
          this.sendFrame(dataURL);
        }, 1000 / fps);
      },
      sendFrame(dataURL) {    
        axios
        .post(`/recognition/stream/`, dataURL)
        .then(() => {
        // Stop the video stream after the first image is sent
        this.stream.getTracks()[0].stop();
        this.stream = null;
         });
        
      },
      Supmit() {    
        axios
        .post(`/recognition/tasks/`, Identifier )
        .then(() => {
        // Stop the video stream after the first image is sent
        this.stream.getTracks()[0].stop();
        this.stream = null;
         });
        
      },
    },
  };
  </script> 

  <!-- <template>
    <div>
      <webcam ref="webcam" :height="480" :width="640" @image="sendImage"></webcam>
    </div>
  </template>
  
  <script>
  import { w3cwebsocket as WebSocket } from 'websocket';
  
  export default {
    data() {
      return {
        ws: null,
      };
    },
    mounted() {
      /* this.ws = new WebSocket('ws://localhost:8000/ws/'); */
      this.ws = new WebSocket('/recognition/ws/');
      this.ws.onopen = () => {
        console.log('WebSocket connection established');
      };
      this.ws.onmessage = (event) => {
        console.log('WebSocket message received:', event.data);
      };
      this.ws.onclose = () => {
        console.log('WebSocket connection closed');
      };
    },
    methods: {
      sendImage(image) {
        const message = {
          type: 'image',
          data: image,
          timestamp: Date.now(),
        };
        this.ws.send(JSON.stringify(message));
      },
    },
  };
  </script>
 -->


<style>
.containerr {
  margin-top: 50px;
}

.video-container {
  margin-top: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  overflow: hidden;
}

video {
  width: 100%;
  height: 500px;
}
</style>