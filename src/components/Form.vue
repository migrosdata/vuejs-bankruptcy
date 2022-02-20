<template>
  <v-form ref="form" v-model="isValid">
    <v-container>
      <v-row>
        <v-col cols="12" md="4">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            v-model.number="form.Asset"
            label="Asset"
            type="number"
            min="0"
            step="1"
            required
            :rules="[v => !!v || 'Asset is required']"
          ></v-text-field>          
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            v-model.number="form.CurAss"
            label="Current Asset"
            required
            :rules="[v => !!v || 'Current Asset is required']"
            type="number"
            min="0"
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            v-model.number="form.Debts"
            label="Debts"
            required
            :rules="[v => !!v || 'Debts is required']"
            type="number"
            min="0"
          ></v-text-field>
        </v-col>  
      </v-row>
      <v-row>
        <v-col cols="12" md="4">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            v-model.number="form.IncDept"
            label="IncDept"
            type="number"
            min="0"
            step="1"
            required
            :rules="[v => !!v || 'IncDept is required']"
          ></v-text-field>          
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            v-model.number="form.Inc"
            label="Inc"
            required
            :rules="[v => !!v || 'Inc is required']"
            type="number"
            min="0"
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            v-model.number="form.Wcfo"
            label="Wcfo"
            required
            :rules="[v => !!v || 'Wcfo is required']"
            type="number"
            min="0"
          ></v-text-field>
        </v-col>  
      </v-row>      
      <v-row>
        <v-col cols="12" md="6">
          <v-btn 
            color="success" 
            class="mr-4" 
            @click="validate"
            :disabled="!isValid">
                Soumettre
          </v-btn>
        </v-col>
        <v-col cols="12" md="6">
          <v-btn color="error" class="mr-4"> Reset</v-btn>
        </v-col>
      </v-row>      
    </v-container>
  </v-form>
</template>

<script>
export default {
  name: "Form",
  data: () => ({
    form: {},
    debtsRules: [
      (v) => v > 0 || "Debts is required"
    ],
    isValid: false
  }),
  props: {
  },
  methods: {
    validate: function () {
      this.$emit("submit", this.form);
    },
  },
};
</script>

<style>
</style>