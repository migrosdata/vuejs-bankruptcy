<template>
  <v-container>
    <transition name="fade">
      <bankruptcy-form v-on:submit="submitHandler" v-if="showForm">
      </bankruptcy-form>
      <error
        v-if="showError"
        v-on:restart="restartHandler"
        :error="this.error"
      ></error>
      <result
        v-if="showResult"
        :reponse="dataikuResponse"
        :companyName="companyName"
        v-on:restart="restartHandler"
      />
    </transition>
  </v-container>
</template>

<script>
// @ is an alias to /src
import BankruptcyForm from "@/components/Form.vue";
import Result from "@/components/Result.vue";
import Error from "@/components/Error.vue";
export default {
  name: "Home",
  components: {
    BankruptcyForm,
    Result,
    Error,
  },
  data: () => ({
    showError: false,
    showForm: true,
    showResult: false,
    dataikuResponse: null,
    companyName: "",
    error: null,
  }),
  mounted() {},
  methods: {
    submitHandler(form) {
      this.showForm = false;
      //this.companyName = form.companyName.toLowerCase();
      delete form.companyName;
      const features = `{ "features" : ${JSON.stringify(form, null, " ")} }`;
      console.log(features.replace("_", "/"));
      this.predictBankruptcy(features);
    },
    restartHandler() {
      this.showResult = false;
      this.showError = false;
      this.dataikuResponse = null;
      this.showForm = true;
    },
    predictBankruptcy(features) {
      this.axios
        .post(
          "https://dataiku.hes-so.ch:8080/public/api/v1/bi21bankruptcy/bankruptcyprediction/predict",
          features
        )
        .then((response) => {
          this.dataikuResponse = response.data;
          console.log(response.data);
          this.showResult = true;
        })
        .catch((error) => {
          this.error = error;
          this.showError = true;
          console.log(error);
        });
    },
  },
};
</script>
<style>
   .fade-enter-active, .fade-leave-active {
      transition: opacity .4s;
   }
   .fade-enter-active, .fade-leave-active /* .fade-leave-active below version 2.1.8 */ {
      opacity: 0;
   }
</style>
