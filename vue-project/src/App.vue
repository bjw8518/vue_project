<script>
import {ref,reactive} from 'vue';
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
export default{
  components:{
    HelloWorld,
    TheWelcome
  },
  setup(){
    const count = ref(0);
    let isButtonDisabled = ref(true);
    const objectAttrs = {
      id: 'container',
      class: 'wrapper'
    }
    const state = reactive({count: 0})

    const items = ref([{message: 'Foo'},{message: 'Bar'}])

    const incresement = () =>{
      count.value +=1;
      isButtonDisabled.value = !isButtonDisabled.value;
    };

    function greet(event, a){
      alert(`안녕 ${items._rawValue[0].message}!`)
      if(event){
        alert(event.target.tagName)
      }
      alert(a)
    }
    //expose to template
    return{
      count,
      incresement,
      isButtonDisabled,
      // objectAttrs
    };
  }
}

</script>

<template>
  <header>
    <!-- <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" /> -->
    <img alt="Vue logo" :class="{logo : count}" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
      <button @click="incresement">{{ count }}</button>
      <div v-bind:id="count"></div>
      <div :id="count"></div>
      <button :disabled="isButtonDisabled">버튼</button>
      <button :disabled="count > 3"> 버튼</button>
      <!-- <div :objectOfAttrs="objectOfAttrs.id"></div> -->
      <!-- {{ count +1 }}
      {{ count > 3 ? '3초과':'3이하' }}
      {{ objectOfAttrs.id.split('').reverse().join('') }} -->
      <h1 v-show="isButtonDisabled">vue는 멋지죠!</h1>
      <h1 v-if="isButtonDisabled">vue는 정말 멋지죠!</h1>
      <h1 v-else>아닌가요??</h1>
      {{ isButtonDisabled == true ? 'vue is Good' : 'vue is Bad' }}
      <li v-for="item in items" :key="item.message">
        {{ index }} - {{ item.message }}
      </li>
      <button @click="greet($event,'A')">환영하기</button>
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
