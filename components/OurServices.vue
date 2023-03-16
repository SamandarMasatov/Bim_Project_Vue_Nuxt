<template>
  <v-container>
    <div id="Services" class="service my-15">
      <v-row style="background-color: #203647 !important" class="pb-5">
        <v-col cols="12" md="12" style="padding-top: 59px">
          <h1 class="servicestitle" style="text-align: center">
            {{ $t('platforma') }}
          </h1>
        </v-col>
        <v-col cols="12" md="5" justify="center">
          <v-card
            elevation="0"
            class="pa-2"
            style="background-color: #203647 !important"
          >
            <p style="color: #fff">
              {{ $t('platform_title') }}
            </p>
          </v-card>
        </v-col>
        <v-col cols="12" md="7">
          <v-row class="fill-height text-center" justify="center">
            <v-col class="model" cols="7" md="4">
              <NuxtLink
                :to="`/${$i18n.locale}/models`"
                style="text-decoration: none !important"
              >
                <v-card
                  class="services_card pa-6"
                  style="
                    background-color: #007cc7 !important;
                    width: 200px !important;
                    height: 200px !important;
                  "
                >
                  <v-img class="ma-4" src="/img/3dmodel.png"></v-img>
                  <h3 class="white--text">{{ $t('modellashtirish') }}</h3>
                </v-card>
              </NuxtLink>
            </v-col>
            <v-col class="model" cols="7" md="4">
              <NuxtLink
                :to="`/${$i18n.locale}/Project`"
                style="text-decoration: none !important"
              >
                <v-card
                  class="services_card pa-8"
                  style="
                    background-color: #007cc7 !important;
                    width: 200px !important;
                    height: 200px !important;
                  "
                >
                  <v-img class="ma-4" src="/img/gotovy_project.png"></v-img>
                  <h3 class="white--text">{{ $t('tayyorLoyiha') }}</h3>
                </v-card>
              </NuxtLink>
            </v-col>
            <v-col class="model" cols="7" md="4">
              <NuxtLink
                :to="`/${$i18n.locale}/Constraction`"
                style="text-decoration: none !important"
              >
                <v-card
                  class="services_card pa-6"
                  style="
                    background-color: #007cc7 !important;
                    width: 200px !important;
                    height: 200px !important;
                  "
                >
                  <v-img class="ma-4" src="/img/konstruksiya.png"></v-img>
                  <h3 class="white--text">{{ $t('konstruksiya') }}</h3>
                </v-card>
              </NuxtLink>
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </div>
  </v-container>
</template>

<script>
export default {
  name: 'OurServicesPage',
}
</script>
<style scoped>
.service {
  background-color: #12232e !important;
}
.services_card {
  border-radius: 0;
  min-height: 250px !important;
  transition: 0.5s;
}
.services_card:hover {
  transform: translate(-10px, -10px);
  box-shadow: 10px 10px 0px #fff !important;
}
.servicestitle:before {
  content: '';
  height: 4px;
  margin-right: 20px !important;
  flex: 1;
  background-color: #fff;
  display: block;
}
.servicestitle {
  display: flex !important;
  align-items: center;
  justify-content: center;
  text-align: center;
  color: #fff;
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 600;
  font-size: 35px;
  line-height: 49px;
  margin-top: 10px;
}
p {
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 400;
  font-size: 14px;
  line-height: 30px;
}
.servicestitle:after {
  content: '';
  height: 4px;
  margin-left: 20px !important;
  flex: 12;
  background-color: #fff;
  display: block;
}
@media only screen and (max-width: 960px) {
  .servicestitle:after {
    content: '';
    height: 4px;
    margin-left: 20px !important;
    flex: 1 !important;
    background-color: #fff;
    display: block;
  }
  p {
    text-align: center !important;
  }
  .model {
    display: flex !important;
    justify-content: center !important;
  }
}
@media (max-width: 570px) {
  h1 {
    font-size: 37px !important;
  }
  p {
    font-size: 18px !important;
  }
}
</style>
