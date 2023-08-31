<template>
    <!-- <v-container class="fill-height" @click="changeBackgroundColor"> -->
    <v-container class="fill-height">
        <v-responsive class="align-center text-center fill-height">
            <h1 class="text-h2 font-weight-bold">Aquí va el TIMER</h1>
        </v-responsive>
    </v-container>
</template>

<script>
  export default {
  methods: {
    changeBackgroundColor() {
      this.$emit('changeColor');
    }
  }
};
</script>
