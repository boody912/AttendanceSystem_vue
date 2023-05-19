<template>
    <div id="app">
      <video ref="video" width="640" height="480"></video>
      <canvas ref="canvas" width="640" height="480" style="display:none;"></canvas>
      <button class="start-camera-btn" v-on:click="startCamera" :disabled="cameraStarted" v-if="!hideStartCamera">Start Camera</button>
      <!-- <button class="upload-pic"  v-if="!hideStartCamera">Upload Picture</button> -->
      <!-- <input class="file-upload" type="file" @change="handleFileUpload">
      <p id="file-name"></p> -->
      <div class="file-upload-container">
        <input class="file-upload" type="file" @change="handleFileUpload">
        <span id="file-name" class="file-name"></span>
      </div>
      <button class="capture-btn" v-on:click="captureImage" :disabled="!cameraStarted" v-if="showCaptureButton">Capture Image</button>
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
        cameraStarted: false,
        showCaptureButton: false,
        hideStartCamera: false
      };
    },
    mounted() {
      this.video = this.$refs.video;
      this.canvas = this.$refs.canvas;
    },
    methods: {
        handleFileUpload(event) {
        const file = event.target.files[0];
        const fileName = file.name;
        const fileNameEl = document.getElementById('file-name');
        fileNameEl.textContent = fileName;
        },
      beforeDestroy() {
        if (this.stream) {
          const tracks = this.stream.getTracks();
          tracks.forEach((track) => {
            track.stop();
          });
           }
        },
      stopCamera: function() {
        if (this.video && this.video.srcObject) {
          const tracks = this.video.srcObject.getTracks();
          tracks.forEach((track) => {
            track.stop();
          });
          this.video.srcObject = null;
          this.cameraStarted = false;
        }
      },
      startCamera: function() {
        var self = this;
        navigator.mediaDevices.getUserMedia({ video: true })
          .then(function(stream) {
            self.video.srcObject = stream;
            self.video.play();
            self.cameraStarted = true;
            self.showCaptureButton = true; // show the capture button after the camera has started
            self.hideStartCamera =true;
          })
          .catch(function(error) {
            alert("Failed to access camera: " + error.message);
          });
      },
      captureImage: function() {
        if (!this.cameraStarted) {
          return;
        }
        var context = this.canvas.getContext('2d');
        context.drawImage(this.video, 0, 0, this.canvas.width, this.canvas.height);
        this.capturedImage = this.canvas.toDataURL();
        this.stopCamera();
        this.sendImage();
      },
      sendImage: function() {
        var self = this;
        if (self.capturedImage) {
          const formData = new FormData();
          formData.append('image', self.capturedImage);
          formData.append('roll', this.$route.params.roll);
          formData.append('class', this.$route.params.class);
         axios
            .post(`/recognition/upload_image/`, formData)                   
            .then(response => {  
              this.beforeDestroy();                
              this.$router.go(-1);
            })           
        }
      },
    },
  };
  </script>
  
  
  
  <style>
  /* .containerr {
    margin-top: 50px;
  } */
  .container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.file-upload-container {
  display: flex;
  align-items: center;
}

.file-name {
  margin-right: 455px;
  font-size: 1.2em;
  color: #555;
}

  .video-container {
    margin-top: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
    overflow: hidden;
  }
  
  .capture-btn {
    display: block;
    margin: 0 auto;
    padding: 10px 270px;
    background-color: rgb(13, 202, 13);
    color: white;
    font-size: 1.2em;
    border: none;
    border-radius: 5px;
  }
  .capture-btn:hover {
    background-color: darkgreen;
  }
  
  .start-camera-btn {
    display: block;
    margin: 0 auto;
    padding: 10px 250px;
    background-color: rgb(0, 0, 255);
    color: white;
    font-size: 1.2em;
    border: none;
    border-radius: 5px;
  }
  .start-camera-btn:hover {
   background-color: rgb(5, 5, 72);
  }
  /* .upload-pic{
    display: block;
    margin: 0 auto;
    margin-top: 10px;
    padding: 10px 140px;
    background-color: #2e8baa      ;
    color: white;
    font-size: 1.2em;
    border: none;
    border-radius: 5px;
  }
  .upload-pic:hover {
   background-color: #083958;
  } */

  .file-upload {
  display: block;
  margin: 0 auto;
  margin-top: 10px;
  margin-left: 455px;

  background-color: #2e8baa;
  color: white;
  font-size: 1.2em;
  border: none;
  border-radius: 5px;
}

.file-upload:hover {
  background-color: #083958;
}

.file-upload::-webkit-file-upload-button {
  visibility: hidden;
}

.file-upload::before {
  content: 'Upload Pic';
  display: inline-block;
  background-color: #2e8baa;
  padding: 10px 140px;
  color: white;
  font-size: 1.2em;
  border: none;
  border-radius: 5px;
}

.file-upload:hover::before {
  background-color: #083958;
}
  
  video {
    width: 100%;
    height: 500px;
  }
  </style>



  



  


   