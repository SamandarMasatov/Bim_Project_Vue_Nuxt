<template> 
<v-app style="background-color: #12232e">
  <Header/>
  <div class="contacts">
    <v-container class="contact">
      <v-row class="pa-0">
        <v-col cols="12" lg="7" class="pa-0 pa-8 map-left">
          <div class="title">{{ $t('aloqa') }}</div>
          <div class="data">
            <v-icon class="icon">mdi-phone</v-icon> +998 (99) 420 - 00 - 16
          </div>
          <div class="data">
            <v-icon class="icon">mdi-email-outline</v-icon> bimloyiha@gmail.com
          </div>
          <div class="map-footer pa-8">
            <div class="title">{{ $t('manzil') }}</div>
            <div class="p">
              <v-icon class="icon">mdi-map-marker</v-icon>
              {{ $t('footer_title') }}
            </div>
          </div>
        </v-col>
        <v-col cols="12" lg="5" class="pa-0 maps">
          <iframe
            src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3176.743586398538!2d67.26957533999797!3d37.23006150922875!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x0%3A0xbf997cff1a48ba97!2zwqtCaW5vIEluc2hvb3QgTWXigJltb3JMb3lpaGHCuyBNQ0hK!5e0!3m2!1sru!2s!4v1659782962023!5m2!1sru!2s"
            style="border: 0"
            allowfullscreen=""
            loading="lazy"
            referrerpolicy="no-referrer-when-downgrade"
          ></iframe>
        </v-col>
      </v-row>
    </v-container>
  </div>
  <Footer/>
  </v-app>
</template> 

<style scoped>
.map-left {
  position: relative;
  height: 500px;
}
@media (max-width: 1264px) {
  .map-left {
    height: 350px;
  }
}
.map-left .icon {
  font-size: 25px;
  transform: translateY(-10%);
}
.map-footer {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
}
.map-footer .p {
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 22px;
  color: #ffffff;
  margin-bottom: 10px;
}
.map-left .title {
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 600;
  font-size: 40px !important;
  line-height: 49px;
  color: #ffffff;
  margin-bottom: 20px;
}
.map-left .data {
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 22px;
  color: #ffffff;
  margin-bottom: 10px;
}
.contacts {
  margin: 180px 0 70px 0;
}
.contact {
  background: #203647;
}
.maps {
  height: 500px;
}
.maps iframe {
  width: 100%;
  height: 100%;
}
</style>
