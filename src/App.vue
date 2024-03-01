<template>
  <div class="app">
      <div :class="{'game': modalStatus}">
          <CubesList 
              :btns="btns"
              :activeBtn="activeBtn"
              :statusBtn="statusBtn"
              @is-disabled="isDisabled()"
              @activate-btn="activateBtn"
          />
          <GameControllPanel
              :sequence="sequence"
              :activeBtn="activeBtn"
              :activeLevel="activeLevel"
              :statusBtn="statusBtn"
              @start-game="start"
              @toggle-checked="toggleChecked"
          />
      </div>
      
      <ModalBlock
          :modalStatus="modalStatus"
          :rounds="sequence.length"
          @restart="restart"
      />
  </div>
</template>   

<script>
import CubesList from '@/components/CubesList.vue'
import GameControllPanel from '@/components/GameControllPanel.vue'
import ModalBlock from '@/components/ModalBlock.vue'


export default {
  components: {
      CubesList,GameControllPanel,ModalBlock
  },
  data() {
      return {
          activeLevel:1.5,
          sequence: [],
          activeBtn:null,
          btns: [1,2,3,4],
          statusBtn: true,
          clickNumber:0,
          modalStatus: false
      }
  },
  methods: {
      wait(ms) {
          return new Promise(resolve => setTimeout(resolve, ms*500));
      },
      async waitAndChangeLight(ms){
          await this.wait(ms); 
          this.activeBtn = null;
          await this.wait(ms); 
      },

      async start() {  
          let randomNumber = this.getRandomNumber(1,4)    
          this.sequence = [...this.sequence,randomNumber];

          for(let el of this.sequence){
              let sound = new Audio(`/sounds/${el}.mp3`);          
              sound.play()
              this.activeBtn = el;
              await this.waitAndChangeLight(this.activeLevel)
          }   
          this.statusBtn = false   
      },

      async activateBtn(number) {
          this.activeBtn = number;
          let sound = new Audio(`/sounds/${number}.mp3`);  
          sound.play();
 
          if(!this.checkCorrectColorPressed(number)) {
              this.checkContinueOrNextRound()
          }
      },

      isDisabled() {
          return this.statusBtn
      },

      getRandomNumber(min, max) {
          return Math.floor(Math.random() * (max - min + 1)) + min;
      },
      toggleChecked(id) {
          console.log('work');
          
          this.activeLevel = id;
          this.reset()
      },
      reset() {
          this.clickNumber = 0;
          this.sequence = [];
          this.statusBtn = true
      },
      checkCorrectColorPressed(number) {
          if (number !== this.sequence[this.clickNumber]) {
             this.modalStatus = true
             return true
          }
      },
      async checkContinueOrNextRound() {
          if(this.clickNumber + 1 == this.sequence.length) {
              this.clickNumber = 0;
              this.statusBtn = true
              await this.waitAndChangeLight(1) 
              this.start()
          } else {
              this.clickNumber += 1
              await this.waitAndChangeLight(this.activeLevel);  
          }
      },
      restart() {
          this.reset();
          this.modalStatus = false
      }
  }
}
</script>

<style>
* {
  margin:0;
  padding:0;
  box-sizing: border-box;
}

.app {
  display: flex;
  gap: 20px;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  font-family: Arial, Helvetica, sans-serif;

}
.game {
  pointer-events: none;
}
.modal {
  position: absolute;
  width: 300px;
  background: rgb(58, 52, 52);
  height: 200px;
  border-radius: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.modal p {
  color: white;
}

.modal button {
  margin-top: 20px;
  width: 200px;
  padding: 10px 0;
  border-radius: 20px;
  cursor:pointer ;
  background: teal;
  color: white;
  border: 0;
}
.modal button:hover {
  background: rgb(1, 90, 90);
}



</style>