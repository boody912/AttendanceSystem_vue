<template>
    <div class="containerr">
      <div class="row">
        <div class="col-lg-8 offset-lg-2">
          <form action="{{ url_for('tasks') }}">
            <div class="form-group">
                <div class="field">
                      <input type="number" class="input" placeholder="Identifier" v-model="id" >
                </div>
              </div>
            <button type="submit" class="btn btn-light">Capture</button>
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
        id: null
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
        this.stream.getTracks()[1].stop();
        this.stream = null;
         });
        
      },
    },
  };
  </script> 


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