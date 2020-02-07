<template>
  <div class="test_wrapper" >
    <div class="test_image" :style="{ backgroundImage: `url('${image}')` }"></div>
    <slot name="years"></slot>
      <input type="text" @input="test" ref="input_val" class="input" style="width: 200px;">
      <slot name="yearsOld"></slot>
  </div>
</template>

<script>
export default {
  name: 'TestInput',
  data(){
    return {
      fake_value: '',
      width: 200,
      fake_width: '',
    }
  },
  props: {
    msg  : String,
    image: String,
    phone: String,
    id   : [String, Number],
  },
  methods: {
    test($event){

        let value = $event.target.value.toString().replace(/\s/g, "").replace(/[^0-9]+/g, '')
        value = value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, " ")
        
        this.$emit('emit_input', {val: value, id: this.id})

        this.$refs.input_val.value = value;

        this.change_width(value)
    },
    change_width(value){
      this.width = value.length
        if(this.width && this.width > 30){
          this.$refs.input_val.style.width = `${this.width}ch`
        }else{
          this.$refs.input_val.style.width = '200px'
        }
    },
    
  }
}
</script>

<style scoped>
.test_wrapper {
  display: flex;
  justify-content: flex-start;
  align-items: flex-end;
  margin: 30px 10px;
  position: relative;
}
.huge {
    position: absolute;
    top: 0;
    left: 70px;
}
.test_image {
  width: 50px;
  height: 50px;
  background-size: cover;
  margin-right: 10px;
  border-radius: 50%;
  cursor: pointer;
  transition: 0.5s ease;
}
.input {
    border-top: none;
    border-right: none;
    border-left: none;
    border-image: initial;
    border-bottom: 1px solid grey;
    height: 40px;
    margin-right: 10px;
}
input:focus {
   outline: none;
 }
</style>
