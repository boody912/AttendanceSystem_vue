<!-- <template>
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
  </script>  -->


<template>
    
    <div id="app">
      <video ref="video" width="640" height="480"></video>
      <canvas ref="canvas" width="640" height="480" style="display:none;"></canvas>
      <div class="field">
          <input type="number" class="input" placeholder="Roll"  v-model="roll">
      </div>
      <button v-on:click="captureImage" >Capture Image</button>
      <div>
        
      </div>
      
    </div>
    <button class="backbutton" onclick="history.back()"> Back</button>

</template>



<script>
import axios from 'axios';

  export default {
    data() {
      return {
        capturedImage: null,
        video: null,
        canvas: null,
        roll:''
        
      };
    },
    mounted() {
        this.video = this.$refs.video;
        this.canvas = this.$refs.canvas;
        this.startCamera();
      
    },
  
    methods: {
      beforeDestroy() {
        if (this.stream) {
          const tracks = this.stream.getTracks();
          tracks.forEach((track) => {
            track.stop();
          });
        }
      },

      /* closeCamera: function() {
          this.stream.getTracks().forEach(function(track) {
            track.stop(); // Stop all tracks in the MediaStream object
          });
          this.showCamera = false; // Hide the camera video element
        }, */

      startCamera: function() {
          var self = this;
          navigator.mediaDevices.getUserMedia({ video: true })
            .then(function(stream) {
              self.video.srcObject = stream;
              self.video.play();
            })
            .catch(function(error) {
              alert("Failed to access camera: " + error.message);
            });
        },
        captureImage: function() {
          var context = this.canvas.getContext('2d');
          context.drawImage(this.video, 0, 0, this.canvas.width, this.canvas.height);
          this.capturedImage = this.canvas.toDataURL();
          
          this.sendImage();
        },
        sendImage: function() {
          var self = this;
          if (self.capturedImage) {
            const formData = new FormData();
                formData.append('image', self.capturedImage);
                formData.append('roll', this.roll);
            axios
              .post(`/recognition/upload_image/`, formData)                   
              .then(response => {  
                this.beforeDestroy();                
                this.$router.push('/courses')
               })
            
          }
        },
      
    },
  };
  </script>


<!-- <script>
    var app = new Vue({
      el: '#app',
      delimiters: ['[[', ']]'],
      data: {
        capturedImage: null,
        video: null,
        canvas: null
      },
      mounted: function() {
        this.video = this.$refs.video;
        this.canvas = this.$refs.canvas;
        this.startCamera();
      },
      methods: {
        startCamera: function() {
          var self = this;
          navigator.mediaDevices.getUserMedia({ video: true })
            .then(function(stream) {
              self.video.srcObject = stream;
              self.video.play();
            })
            .catch(function(error) {
              alert("Failed to access camera: " + error.message);
            });
        },
        captureImage: function() {
          var context = this.canvas.getContext('2d');
          context.drawImage(this.video, 0, 0, this.canvas.width, this.canvas.height);
          this.capturedImage = this.canvas.toDataURL();
          this.sendImage();
        },
        sendImage: function() {
          var self = this;
          if (self.capturedImage) {
            $.ajax({
              url: '{% url "upload_image" %}',
              type: 'POST',
              data: {
                'image': self.capturedImage
              },
              success: function(response) {
                console.log(response);
              },
              error: function(error) {
                console.log(error);
              },
            });
          }
        },
      }
    });
  </script> -->


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