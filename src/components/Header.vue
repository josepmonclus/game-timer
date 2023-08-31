<template>
    <v-container :style="{ backgroundColor: backgroundColor, color: fontColor }">
        <v-text-field 
          class="inputSeconds"
          label="Seconds"
          v-model="seconds"
          prepend-icon="mdi-camera-timer"
          :min="10"
          :max="300"
          type="number"
          :rules="secondsRules"
        ></v-text-field>
      </v-container>
</template>

<script setup>
  //
</script>

<style>
.inputSeconds input[type='number'] {
    -moz-appearance:textfield;
}
.inputSeconds input::-webkit-outer-spin-button,
.inputSeconds input::-webkit-inner-spin-button {
    -webkit-appearance: none;
}
</style>