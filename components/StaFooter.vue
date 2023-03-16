<template>
  <div style="background-color: #203647 !important; padding: 14px 0">
    <div class="f-container">
      <v-row justify="center">
        <v-col cols="11" sm="8" md="8" class="d-inline-flex align-center">
          <div class="img">
            <v-img class="footerimg" src="/img/bim-logo-white.png"></v-img>
          </div>
          <span class="footer-title">
            {{ $t('footer_title') }}
          </span>
        </v-col>
        <v-col cols="11" sm="4" md="4" class="footer-link">
          <ul class="footer_link_in">
            <li>
              <nuxt-link :to="`/${$i18n.locale}`">{{ $t('uy') }}</nuxt-link>
            </li>
            <li>
              <nuxt-link :to="`/${$i18n.locale}/AboutUs`" class="link">{{
                $t('biz_haqimizda')
              }}</nuxt-link>
            </li>
            <li>
              <nuxt-link :to="`/${$i18n.locale}/Contact`" class="link">{{
                $t('portfolio')
              }}</nuxt-link>
            </li>
          </ul>
        </v-col>
      </v-row>
    </div>
  </div>
</template>
<script>
export default {
  name: 'FooterPage',
}
</script>

<style scoped>
.f-container {
  width: 1300px;
  padding: 0 20px;
  margin: 0 auto;
}
.footer_link_in {
  text-align: right;
}
.footer-title {
  max-width: 428px;
  margin-left: 72px;
}
.img {
  width: 100px;
  height: 92px;
}
.footerimg {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
p {
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 400;
  font-size: 15px;
  line-height: 30px;
}
a {
  text-decoration: none !important;
  color: #fff !important;
  transition: all 0.5s ease !important;
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 30px;
}
a:hover {
  color: #007cc7 !important;
}

p {
  color: white !important;
}
li {
  margin: 10px 0 !important;
  list-style: none !important;
}
@media (max-width: 570px) {
  a {
    font-size: 16px;
  }
  p {
    font-size: 18px;
  }
  .footerimg {
    width: 150px !important;
  }
}
.footer-link {
  display: flex;
  justify-content: end !important;
}
</style>
