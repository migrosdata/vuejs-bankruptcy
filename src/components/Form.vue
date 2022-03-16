<template>
  <v-form ref="form" v-model="isValid">
    <v-container>
      <v-row>
        <v-col cols="12" md="4">
          <v-slider
            :prepend-icon="riskIcon"
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
            v-model.number="form.CURASS"
            label="Current Asset"
            required
            :rules="[(v) => !!v || 'Current Asset is required']"
            type="number"
            min="0"
          ></v-text-field>
        </v-col>
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
      </v-row>
      <v-row>
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
        <v-col cols="12" md="3">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            label="ASSETS/DEBTS"
            v-model.number="ASSETS_DEBTS"
            value="4"
            type="number"
            disabled
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="3">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            v-model.number="CURASS_ASSETS"
            label="CURASS/ASSETS"
            type="number"
            disabled
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="3">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            v-model.number="CURASS_CURDEBTS"
            label="CURASS/CURDEBTS"
            type="number"
            disabled
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="3">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            v-model.number="CURDEBTS_DEBTS"
            label="CURDEBTS/DEBTS"
            type="number"
            disabled
          ></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12" md="3">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            v-model.number="INC_ASSETS"
            label="INC/ASSETS"
            type="number"
            disabled
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="3">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            v-model.number="INC_DEBTS"
            label="INC/DEBTS"
            type="number"
            disabled
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="3">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            v-model.number="WCFO_ASSETS"
            label="WCFO/ASSETS"
            type="number"
            disabled
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="3">
          <v-text-field
            prepend-icon="mdi-currency-usd"
            v-model.number="WCFO_DEBTS"
            label="WCFO/DEBTS"
            type="number"
            disabled
          ></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-col class="d-flex" cols="12" md="12">
          <v-spacer></v-spacer>
          <v-btn color="error" class="mr-4" @click="reset"
            >Reset <v-icon right dark>mdi-restart</v-icon></v-btn
          >
          <v-btn
            color="success"
            class="mr-4"
            @click="validate"
            :disabled="!isValid"
          >
            Soumettre
          </v-btn>
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
    riskIcon: {
      get() {
        return this.form.risk > 50
          ? this.form.risk > 95
            ? "mdi-emoticon-devil-outline"
            : "mdi-emoticon-cool-outline"
          : "mdi-emoticon-confused-outline";
      },
    },
    ASSETS_DEBTS: {
      get() {
        if (this.form.ASSETS || this.form.DEBTS) {
          return this.form.ASSETS / this.form.DEBTS;
        } else {
          return null;
        }
      },
    },
    CURASS_ASSETS: {
      get() {
        if (this.form.CURASS || this.form.ASSETS) {
          return this.form.CURASS / this.form.ASSETS;
        } else {
          return null;
        }
      },
    },
    CURASS_CURDEBTS: {
      get() {
        if (this.form.CURASS || this.form.CURDEBTS) {
          return this.form.CURASS / this.form.CURDEBTS;
        } else {
          return null;
        }
      },
    },
    CURDEBTS_DEBTS: {
      get() {
        if (this.form.CURDEBTS || this.form.DEBTS) {
          return this.form.CURDEBTS / this.form.DEBTS;
        } else {
          return null;
        }
      },
    },
    INC_ASSETS: {
      get() {
        if (this.form.ASSETS || this.form.INC) {
          return this.form.INC / this.form.ASSETS;
        } else {
          return null;
        }
      },
    },
    INC_DEBTS: {
      get() {
        if (this.form.INC || this.form.DEBTS) {
          return this.form.INC / this.form.DEBTS;
        } else {
          return null;
        }
      },
    },
    WCFO_ASSETS: {
      get() {
        if (this.form.WCFO || this.form.ASSETS) {
          return this.form.WCFO / this.form.ASSETS;
        } else {
          return null;
        }
      },
    },
    WCFO_DEBTS: {
      get() {
        if (this.form.WCFO || this.form.DEBTS) {
          return this.form.WCFO / this.form.DEBTS;
        } else {
          return null;
        }
      },
    },
  },
  methods: {
    validate() {
      this.$emit("submit", this.prepareData());
    },
    reset() {
      this.$refs.form.reset();
    },
    prepareData() {
      return {
        ASSETS_DEBTS: this.ASSETS_DEBTS,
        CURASS_ASSETS: this.CURASS_ASSETS,
        CURASS_CURDEBTS: this.CURASS_CURDEBTS,
        CURDEBTS_DEBTS: this.CURDEBTS_DEBTS,
        INC_ASSETS: this.INC_ASSETS,
        INC_DEBTS: this.INC_DEBTS,
        WCFO_ASSETS: this.WCFO_ASSETS,
        WCFO_DEBTS: this.WCFO_DEBTS,
        risk: this.form.risk,
      };
    },
  },
};
</script>

<style>
</style>