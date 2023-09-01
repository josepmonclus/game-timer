<template>
  <v-app :style="{ backgroundColor: backgroundColor, color: fontColor }">
    <v-main>
      <v-container class="header">
        <v-text-field 
          class="inputSeconds"
          label="Seconds"
          v-model="inputSecondsValue"
          :min="10"
          :max="300"
          type="number"
          :rules="secondsRules"
        ></v-text-field>
      </v-container>
      <v-container class="main" @click="startTimer">
        <v-responsive class="align-center text-center fill-height">
          <p class="text-h5">TAP TO {{ timerActive ? 'STOP' : 'START' }}</p>
          <p class="text-h1 font-weight-bold">{{ secondsTimer }} s</p>
        </v-responsive>
      </v-container>
      <v-container class="footer align-center text-center">
        <p class="text-subtitle-1">Made by Josep Monclús</p>
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
 //
</script>

<script>
  const colorPalette = [
    ['#FF595E', '#8AC926'],
    ['#FFCA3A', '#3B6FFF'],
    ['#8AC926', '#6A4C93'],
    ['#1982C4', '#FF595E'],
    ['#6A4C93', '#FFCA3A'],
  ]
  export default {
    data() {
      return {
        currentColorIndex: 1,
        backgroundColor: colorPalette[1][0],
        fontColor: colorPalette[1][1],
        inputSecondsValue: 60,
        minSeconds: 10,
        maxSeconds: 300,
        secondsRules: [
          value => !!value || 'Seconds is required!',
          value => value >= this.minSeconds || 'Min timer is ' + this.minSeconds + ' seconds',
          value => value <= this.maxSeconds || 'Max timer is ' + this.maxSeconds + ' seconds'
        ],
        secondsTimer: 60,
        timerActive: false,
        timerInterval: null,
      }
    },
    mounted() {

    },
    methods: {
      changeBackgroundColor() {
        if(this.currentColorIndex == colorPalette.length - 1) {
          this.currentColorIndex = 0
        } else {
          this.currentColorIndex = this.currentColorIndex + 1
        }
        this.backgroundColor = colorPalette[this.currentColorIndex][0]
        this.fontColor = colorPalette[this.currentColorIndex][1]
      },
      startTimer() {
        if(this.inputSecondsValue && this.inputSecondsValue >= this.minSeconds && this.inputSecondsValue <= this.maxSeconds) {
          if(this.timerActive) {
            clearInterval(this.timerInterval);
            this.timerActive = false;
            this.secondsTimer = this.inputSecondsValue
          } else {
            this.secondsTimer = this.inputSecondsValue
            
            this.timerInterval = setInterval(() => {
              if (this.secondsTimer > 0) {
                this.secondsTimer--;
              } else {
                clearInterval(this.timerInterval);
                this.timerActive = false;
              }
            }, 1000);
            this.timerActive = true;
            this.changeBackgroundColor();
          }
        }
      }
    }
  }
</script>

<style>
.header {
  height: 10%
}

.main {
  height: 84%
}

.footer {
  height: 5%
}

.v-text-field input {
    font-size: 1.5em;
  }

.inputSeconds input[type='number'] {
    -moz-appearance:textfield;
}
.inputSeconds input::-webkit-outer-spin-button,
.inputSeconds input::-webkit-inner-spin-button {
    -webkit-appearance: none;
}
</style>