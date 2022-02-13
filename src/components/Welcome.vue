<template>
  <base-card>
    <v-img
        :src="require('../assets/bankruptMan.png')"
        class="grey lighten-2"
        max-height="950"      
        contain  
        position="top"
    >
      <v-row
        class="fill-height pa-3"
        align="center"
      >
        <v-col
          cols="12"
          md="7"
          offset-md="5"
        >
          <h1 class="display-3 font-weight-light">
            Bankruptcy
          </h1>

          <div class="subheading text-uppercase pl-2 mb-4">
            yo
          </div>

          <v-btn
            color="primary"
            depressed
            to="/home"
          >
            ba
          </v-btn>
        </v-col>
      </v-row>
    </v-img>
  </base-card>
</template>

<script>
  export default {
    name: 'Welcome',
  }
</script>
