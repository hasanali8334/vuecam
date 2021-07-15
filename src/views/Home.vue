<template>
  <div class="home">
    
    
    <video class="player"></video>
    <button @click="opencam()">Open Cam</button>
    <button @click="record()">Record</button>
  </div>
</template>

<script>
// @ is an alias to /src
let recordrtc =require('recordrtc');

export default {
  


  data() {
    return{
    stream:null,
    video:null,
    recorder:null,
    }
  },
  
  methods: {
    opencam: async function(){
      console.log("opencam çalıştı");
     this.stream=await navigator.mediaDevices.getUserMedia({ audio: true, video:true});
     this.recorder = new recordrtc(this.stream, {type: 'video'});
      this.video=document.querySelector('.player');
      this.video.srcObject=this.stream;
      this.video.play();
      this.recorder.addEventListener('dataavailable', function(event) { console.log(event.data) })
     

     
  },
  watch: {


  },
  record: async function(){
   
this.recorder.StartRecording();

  }
},
}

</script>
