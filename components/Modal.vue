<!--  -->
<template>
  <div>
    <p v-if="props.node"><span class="title">{{props.node.tipId}}</span> <span class="close" @click="close">X</span></p>
  </div>
</template>

<script >

export default {
  name: '',
  props: {
    props: {
      type: Object,
      require: true,
    },
  },
  methods:{
      close(){
          this.$emit('close')
      }
  },
  created(){
      console.log(this.props)
  },
  mounted(){ console.log(this.props)},

}
</script>
<style lang='scss' scoped>
p {
  text-align: center;
  .title{
      font-size: 36px;
      font-weight: bold;
  }
  .close {
    float: right;
    padding: 8px;
    cursor: pointer;
  }
}
</style>