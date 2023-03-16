<template>
  <v-app style="background-color: #12232e">
    <div>
      <Header />
      <Home />
      <OurServices />
      <About />
      <OurProject />
      <OurStore />
      <v-container class="mt-10 pa-0">
        <Serti class="mobil" />
      </v-container>
      <Maps />
      <Footer />
    </div>
  </v-app>
</template>

<script>
export default {
  name: 'IndexPage',
}
</script>

<style>
@media (min-width: 1904px){
    .container {
      max-width: 1360px !important;
  }
  }
html {
  scroll-behavior: smooth;
}
@media (max-width: 500px) {
  .mobil {
    padding-top: 30px !important;
  }
}
</style>

95 772 32 95 Ergash

99 175 19 78 Mohi opa