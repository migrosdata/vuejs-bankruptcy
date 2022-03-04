<template>
  <v-form ref="form" v-model="isValid">
    <v-container>
      <v-row>
        <v-col cols="12" md="4">
          <v-slider
            prepend-icon="mdi-human"
            v-model="form.risk"
            hint="Choose your investor profile"
            label="Risk"
            thumb-color="red"
          ></v-slider>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12" md="4">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            v-model.number="form.ASSETS"
            label="Asset"
            type="number"
            min="0"
            step="1"
            required
            :rules="[(v) => !!v || 'Asset is required']"
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            v-model.number="form.CFFO"
            label="Cash flow from operations"
            required
            :rules="[(v) => !!v || 'Cash flow from operations is required']"
            type="number"
            min="0"
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            v-model.number="form.CURASS"
            label="Current Asset"
            required
            :rules="[(v) => !!v || 'Current Asset is required']"
            type="number"
            min="0"
          ></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12" md="4">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            v-model.number="form.CURDEBTS"
            label="Current Debts"
            required
            :rules="[(v) => !!v || 'Current Debts is required']"
            type="number"
            min="0"
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            v-model.number="form.DEBTS"
            label="Debts"
            required
            :rules="[(v) => !!v || 'Debt is required']"
            type="number"
            min="0"
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            v-model.number="form.INC"
            label="Income"
            type="number"
            min="0"
            step="1"
            required
            :rules="[(v) => !!v || 'Income is required']"
          ></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12" md="4">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            v-model.number="form.INCDEPT"
            label="Income plus depreciation"
            required
            :rules="[(v) => !!v || 'Income plus depreciation is required']"
            type="number"
            min="0"
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            v-model.number="form.SALES"
            label="Sales"
            required
            :rules="[(v) => !!v || 'Sales is required']"
            type="number"
            min="0"
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            v-model.number="form.WCFO"
            label="Working capital from operation"
            required
            :rules="[
              (v) => !!v || 'Working capital from operation is required',
            ]"
            type="number"
            min="0"
          ></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12" md="4">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            label="ASSETS/DEBTS"
            v-model.number="ASSETS_DEBTS"
            value="4"
            type="number"
            disabled
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            :value="form.CURASS / form.CURDEBTS"
            label="CURASS/CURDEBTS"
            type="number"
            disabled
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            :value="form.INCDEPT / form.DEBTS"
            label="INCDEPT/DEBTS"
            type="number"
            disabled
          ></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12" md="4">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            :value="form.WCFO / form.DEBTS"
            label="WCFO/DEBTS"
            type="number"
            disabled
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            :value="form.INC / form.DEBTS"
            label="INC/DEBTS"
            type="number"
            disabled
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            :value="form.INC / form.ASSETS"
            label="INC/ASSETS"
            type="number"
            disabled
          ></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12" md="6">
          <v-btn
            color="success"
            class="mr-4"
            @click="validate"
            :disabled="!isValid"
          >
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
    features: {},
    isValid: false,
  }),
  props: {},
  computed: {
    ASSETS_DEBTS: {
      get() {
        return this.form.ASSETS / this.form.DEBTS;
      },
    },
  },
  methods: {
    validate() {
      this.$emit("submit", this.prepareData());
    },
    prepareData() {
      return { ASSETS_DEBTS: this.ASSETS_DEBTS };
    },
  },
};
</script>

<style>
</style>