<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/bankruptMan.png" height="200" />
    <bankruptcy-form v-on:submit="submitHandler" v-if="showForm">
    </bankruptcy-form>
    <error v-if="showError" v-on:restart="restartHandler"></error>
    <result
      v-if="showResult"
      :reponse="dataikuResponse"
      v-on:restart="restartHandler"
    />
  </div>
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
  }),
  mounted() {
    //TODO:loin
    console.log(process.env.VUE_APP_API);
    console.log("yo");
  },
  methods: {
    submitHandler(form) {
      this.showForm = false;
      const features = `{ "features" : ${JSON.stringify(form, null, " ")} }`;
      console.log(features);
      console.log(features.replace("_", "/"));
      this.predictBankruptcy(features);
    },
    restartHandler() {
      this.showResult = false;
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
          this.showSpinner = false;
          this.showResult = true;
        })
        .catch((error) => {
          this.showSpinner = false;
          this.showError = true;
          console.log(error);
        });
    },
  },
};
</script>
