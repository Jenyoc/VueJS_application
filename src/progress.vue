<template>
  <div class="progress">
  <div class="progress-bar" v-bind:style="width"></div>
  </div>
</template>
<script>
  export default {
    props:{
      max:Number,
      val:Number
    },
    computed:{
      width(){
        let w=this.val/this.max*100;
        return{
          width:w+'%'
        }
      }
    }
  }
</script>
