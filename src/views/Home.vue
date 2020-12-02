<template>
 <v-img
    dark
    src="https://gniktest-com.stackstaging.com/wp-content/uploads/2020/08/3.png"
    class="item"
  >
    <v-row
      align="center"
      justify="center"
    >
      <v-col
        class="text-center"
        cols="12"
      >
      <div class="carousel-data">
        <h1 class="display-4 font-weight-normal">
          Connecting Business Needs
        </h1>
        <h2 class="font-weight-light">
          Trusted Sources, Lasting Relationships
        </h2>
        <div class="center">
          <h3 class="subheading text-uppercase mr-4">
          Lets Talk
          </h3>
          <h3 class="subheading text-uppercase ml-4">
          Our Services
          </h3>
        </div>
      </div>
      </v-col>
    </v-row>
  </v-img>
</template>

<script>
export default {
  data: () => ({
    items: [
      {
        src: 'https://gniktest-com.stackstaging.com/wp-content/uploads/2020/08/3.png'
      }
    ]
  })
}
</script>
<style scoped>
.carousel-data > * {
  margin-bottom: 50px;
}
.item {
  height:93vh !important;
  display: flex;
  justify-content: center;
  align-items: center;
}
.center {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
