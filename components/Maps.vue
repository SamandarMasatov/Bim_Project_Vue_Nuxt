<template>
  <v-container id="Map" class="mt-16 mb-16">
    <v-row style="background-color: #203647 !important">
      <v-col cols="12" md="12" style="padding-top: 59px">
        <h1 class="maptitle">{{ $t('set') }}</h1>
      </v-col>
      <v-col cols="12" md="2" class="messengers">
        <div class="messenger_mobile d-flex d-md-none">
          <a class="facebook_mobile d-flex d-md-none" href="#"
            ><i class="telegram fa-brands fa-facebook"></i
          ></a>
          <a class="youtube_mobile d-flex d-md-none" href="#"
            ><i class="instagram fa-brands fa-instagram"></i
          ></a>
          <a class="telegram_mobile d-flex d-md-none" href="#"
            ><i class="youtube fa-brands fa-youtube"></i
          ></a>
          <a class="instagram_mobile d-flex d-md-none" href="#"
            ><i class="telegram fa-brands fa-telegram"></i
          ></a>
        </div>
        <a class="facebook d-none d-md-flex" href="#"
          ><i class="telegram fa-brands fa-facebook"></i
        ></a>
        <a class="youtube d-none d-md-flex" href="#"
          ><i class="instagram fa-brands fa-instagram"></i
        ></a>
        <a class="telegram d-none d-md-flex" href="#"
          ><i class="youtube fa-brands fa-youtube"></i
        ></a>
        <a class="instagram d-none d-md-flex" href="#"
          ><i class="telegram fa-brands fa-telegram"></i
        ></a>
      </v-col>
      <v-col class="maps" cols="12" md="10">
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
</template>

<script>
export default {
  name: 'MapsPage',
}
</script>

<style scoped>
.messengers {
  display: flex !important;
  align-items: center !important;
  justify-content: space-around !important;
  flex-direction: column !important;
}
.messenger_mobile a {
  margin: 0 15px !important;
}
.messengers a {
  margin: 20px 0;
}
.messengers a i {
  color: #fff !important;
  transition: all 0.5s ease !important;
  font-size: 50px !important;
}
.messengers a {
  text-decoration: none !important;
}
.messengers a .facebook:hover {
  color: #1877f2 !important;
}
.messengers a .instagram:hover {
  color: #e1306c !important;
}
.messengers a .youtube:hover {
  color: #ff0000 !important;
}
.messengers a .telegram:hover {
  color: #0088cc !important;
}
.maptitle:before {
  content: '';
  height: 4px;
  margin-right: 20px !important;
  flex: 1;
  background-color: #fff;
  display: block;
}
.maptitle {
  display: flex !important;
  text-align: center !important;
  align-items: center;
  color: #fff;
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 600;
  font-size: 40px;
  line-height: 49px;
}
.maptitle:after {
  content: '';
  height: 4px;
  margin-left: 20px !important;
  flex: 12;
  background-color: #fff;
  display: block;
}
iframe {
  width: 100% !important;
  height: 100% !important;
}
.maps {
  height: 400px !important;
}
@media only screen and (max-width: 960px) {
  .messengers {
    width: 100% !important;
    display: flex !important;
    align-items: center !important;
    justify-content: space-between !important;
    flex-direction: column-reverse !important;
  }
  .maptitle:after {
    content: '';
    height: 4px;
    margin-left: 20px !important;
    flex: 1 !important;
    background-color: #fff;
    display: block;
  }
}
@media (max-width: 570px) {
  h1 {
    font-size: 37px !important;
  }
}
</style>
