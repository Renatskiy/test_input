<template>
  <div id="app" >
    <div v-for="(item, index) in users" :key="index" @click="click(index)" 
        :class="{active: item.active}">
      <StandartInput v-bind="item" @emit_input='emit_input' >
        <template #years> <span class="huge">HUGE IS</span></template>

        <template #yearsOld>hours old</template>
      </StandartInput>
    </div>
  </div>
</template>

<script>
import StandartInput from './components/ui_input.vue'

export default {
  name: 'app',
  data(){
    return {
      users: [
        {
          image: require("./assets/images/alf.jpg"),
          phone: '',
          id: 1,
          active: false,
        },
        {
          image: require("./assets/images/alf.jpg"),
          phone: '',
          id: 2,
          active: false,
        },
        {
          image: require("./assets/images/alf.jpg"),
          phone: '',
          id: 3,
          active: false,
        },
      ]
    }
  },
  components: {
    StandartInput
  },
  computed: {
    imput_props({image, input_value}){
      return {
        image,
        input_value
      }
    }
  },
  methods: {
    emit_input(obj){
      const {id, val} = obj
      const user =  this.users.find(user => user.id === id)
      user.phone = val
    },
    click(index){
      this.users.forEach(user => {
          return user.active = false
      });
      this.users[index].active = true;
    }
  }
}
</script>

<style >
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.active .test_image {
    border: 1px solid blue;
  
}
</style>
