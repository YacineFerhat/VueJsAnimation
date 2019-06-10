<template>
  <div class="hero">
    <div class="hero-body">   
      <div class="container">
        <div class="columns is-centered">
          <div class="column is-half">
            <h1 class="title is-1 has-text-centered">  
              The Super Quiz
            </h1>
          </div>
           </div>
          <hr>
          <div class="columns is-centered ">
            <div class="column is-half">
              <transition name="flip" mode="out-in">
                <component :is="mode" @confirmed="mode='app-Question'" @answered="answered($event)">
                </component>
              </transition>
              
            </div>
          </div>
        
      </div>
    </div>
  </div>
</template>


<script>

import Answer from './components/Answer';
import Question from './components/Question';

export default {

  data(){
    return{
      mode : 'app-Question'
    }
  },
 
  components:{
    appAnswer : Answer,
    appQuestion : Question
  },

  methods: {
    answered(isCorrect){
      if(isCorrect){
        this.mode='app-Answer';

      }
      else{
        this.mode='app-Question';
        alert('Wrong, try again')
      }
    }
  }
}
</script>

<style>
  .flip-enter {
    transform: rotateY(0deg);
  }

  .flip-enter-active{
    animation: flip-in 1s ease-out forwards;
  }

  .flip-leave {
    transform: rotateY(0deg);
  }

  .flip-leave-active {
    animation: flip-out 1s ease-out forwards;
  }

  @keyframes flip-out {
    from {
      transform: rotateY(0deg);
    }
    to{
      transform: rotateY(90deg);
    }
  }

  @keyframes flip-in {
    from{
      transform: rotateY(90deg);
    }
    to{
      transform: rotateY(0deg);
    }
  }
</style>
