<template>
  <v-container>
                <v-col cols="12" md="3">
                <h1 class="display-4">{{ this.reponse.result.probaPercentile}} % </h1>
            </v-col>
        </v-row>
    <div>
      {{ this.reponse.result.prediction }}
    </div>
        <v-row>
            <v-col>
                <v-btn
                    @click="restart"
                >
                    Nouvelle prédiction
                    <v-icon large>mdi-bicycle</v-icon>            
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