<template>
  <div>
    <h1 style="text-align: center">VueJS</h1>
    <h2 style="text-align: center">всякие плюшки на фреймворке</h2>
    <br><hr><br>
    <div>
      Enter your city:
      <input type="text"
             v-bind:value="name"
             v-on:input="name=$event.target.value"
             v-text="">
      <p><b>City: {{name}}</b></p>
      <br><hr><br>
      <button v-on:click="addNum(numbers)" class="btn btn-success">+ number (1-10)</button>
      <button v-on:click="delNum(numbers)" class="btn btn-danger">- number (1-10)</button>
      <app-progress v-bind:val="numbers.length"
                    v-bind:max="maxNumbers">
      </app-progress>
      <ul class="l-g">
        <transition-group name="liNum">
          <li v-bind:key="0"
              class="l-g-i"
              v-for="number in numbers">
            {{number}}
          </li>
        </transition-group>
      </ul>
    </div>
    <br><hr><br>
    <div>
      <h2>Price-counter</h2>
      <p>Current price: {{price}}</p>
      <p><input type="text" v-model="price"></p>
      <button class="min" v-on:click="onMinus">-</button>
      <input class="val" v-bind:value="cnt" v-on:change="onInpNumber($event.target.value)">
      <button class="plus" v-on:click="onPlus">+</button>
      <h3 class="total">{{total}}</h3>
    </div>
  </div>
</template>
<script>
  import Progress from './progress.vue'
  export default {
    data() {
      return {
        name: '',
        numbers: [],
        count: 0,
        maxNumbers: 10,
        cnt: 1,
        price: 1337
      }
    },
    methods: {
      addNum(nums) {
        let rnd = () => {
          return parseInt(Math.random() * 11)
        };
        if (nums.length < 10) {
          nums.push(rnd());
        }
      },
      delNum(nums) {
        delete nums.pop();
      },
      onMinus(){
        if(this.cnt > 1){
          this.cnt--;
        }
      },
      onPlus(){
        if(this.cnt < 10){
          this.cnt++;
        }
      },
      onInpNumber(newVal){
        let num = parseInt(newVal);

        if(isNaN(num)||num<1){num=1}
        if(num>10){num=10}

        this.cnt = num;
        this.$forceUpdate();
      }
    },
    components: {
      AppProgress: Progress
    },
    computed: {
      total(){return this.cnt*this.price}
    }
  }
</script>
<style scoped>
  .liNum-enter {
    color: black;
    opacity: 0;
  }

  .liNum-enter-active {
    color: green;
    transition: opacity 0.5s;
  }

  .liNum-leave-active {
    color: black;
    transition: opacity 0.5s;
  }

  .liNum-leave-to {
    color: red;
    opacity: 0;
  }

  .progress {
    margin: 15px;
  }
</style>
