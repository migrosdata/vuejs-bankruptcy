<template>
  <v-container>
    <v-row align="center" justify="center">
      <v-col cols="12" md="12" >
        <div v-if="this.reponse.result.prediction == 1" class="green accent-4 text-h6">
          <h1>
            <v-icon x-large>mdi-bank-check</v-icon> 
            {{ this.reponse.result.probaPercentile }} % Healthy company!</h1>
        </div>
        <div v-else class="red accent-4" >
          <h1>
            <v-icon x-large>mdi-bank-off-outline</v-icon>
            {{ this.reponse.result.probaPercentile }} %
            Risk of bankruptcy!
          </h1>
        </div>
      </v-col>
    </v-row>
    <v-row justify="center" align="center">
      <v-col cols="12" md="4" align="center">
        <v-btn @click="restart">
          Nouvelle prédiction
          <v-icon large>mdi-piggy-bank</v-icon>
        </v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "Result",
  props: {
    reponse: {
      type: Object,
      required: true,
    },
  },
  methods: {
    restart: function () {
      this.$emit("restart");
    },
  },
};
</script>

<style>
</style>