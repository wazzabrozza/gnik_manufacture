<template>
 <v-app>
   <div>
    <v-app-bar
      color="white"
      style="z-index:2;"
    >
      <div>
      <v-img :src="require('./assets/gnik-dark-logo.png')" width="60px"
    ></v-img>
      </div>
      <v-spacer></v-spacer>
       <v-btn
         to="/"
        text
      >
        <span >Home</span>
      </v-btn>
         <v-btn
        text
      >
        <span >Sign in/Sign up</span>
      </v-btn>
       <v-btn
         to="/catalogue"
        text
      >
        <span >Find your product</span>
      </v-btn>
      <v-btn
        text
      >
        <span>Trends Forecasts</span>
      </v-btn>
       <v-btn
        text
      >
        <span >gnik Solutions</span>
      </v-btn>
       <v-btn
        text
      >
        <span >About</span>
      </v-btn>
       <v-btn
        text
      >
        <span >FAQ's</span>
      </v-btn>
       <v-btn
        text
        to="/dashboard"
      >
        <span>Dashboard</span>
      </v-btn>
       <v-divider
      class="mx-4"
      vertical
    ></v-divider>
       <span class="mr-2">Manufacturer</span>
     <v-avatar color="red" size="40">
      <span class="white--text headline">M</span>
    </v-avatar>

    </v-app-bar>
    <router-view/>
  </div>
  </v-app>
</template>

<script>
export default {
  name: 'App',
  data: () => ({
    //
  })
}
</script>
