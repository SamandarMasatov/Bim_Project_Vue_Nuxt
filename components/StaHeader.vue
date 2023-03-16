<template>
  <!-- Header wrapper -->
  <div class="header" :class="header ? 'header-active' : ''">
    <div
      class="lang_cover"
      @click="langBtnRemove"
      :class="{ lang_active: lanActive }"
    ></div>
    <!-- Header in -->
    <v-container
      class="header_in d-flex justify-space-between white--text transparent"
      style="align-items: center"
    >
      <!-- pages link -->
      <div class="links d-flex">
        <nuxt-link :to="`/${$i18n.locale}`" class="link">{{
          $t('uy')
        }}</nuxt-link>
        <nuxt-link :to="`/${$i18n.locale}/AboutUs`" class="link">{{
          $t('biz_haqimizda')
        }}</nuxt-link>
        <nuxt-link :to="`/${$i18n.locale}/Contact`" class="link">{{
          $t('portfolio')
        }}</nuxt-link>
      </div>
      <!-- Shop btn and lang btn -->
      <span class="d-flex">
        <div
          class="drop_menu"
          :class="{ clickdropmenu: cdmactive }"
          @click="dropClick"
        >
          <i class="fa-solid fa-cart-shopping"></i>

          <span>{{ $t('dukon') }}</span>

          <ul class="drop_down" :class="{ dropDownActive: cddac }">
            <li>
              <NuxtLink :to="`/${$i18n.locale}/Project`" class="drop_link">{{
                $t('tayyorLoyiha')
              }}</NuxtLink>
            </li>
            <li>
              <NuxtLink :to="`/${$i18n.locale}/models`" class="drop_link"
                >{{ $t('dModel') }}
              </NuxtLink>
            </li>
            <li>
              <NuxtLink
                :to="`/${$i18n.locale}/Constraction`"
                class="drop_link"
                >{{ $t('konstruksiya') }}</NuxtLink
              >
            </li>
          </ul>
        </div>

        <div class="lang_btn" @click="langBtn">
          <span>{{ $i18n.locale }}</span>
          <ul class="lang_down" :class="{ lang_active: lanActive }">
            <li @click.prevent="$i18n.setLocale('uz')">UZ</li>
            <li @click.prevent="$i18n.setLocale('ru')">RU</li>
            <li @click.prevent="$i18n.setLocale('en')">EN</li>
          </ul>
        </div>
      </span>
    </v-container>

    <div class="img-logo">
      <div class="relative" :class="header ? 'img-logo-active' : ''">
        <NuxtLink :to="`/${$i18n.locale}/`">
          <img
            src="/img/bim-logo-white.png"
            width="100%"
            height="100%"
            alt="logo"
          />
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  naem: 'HeaderPage',
  data() {
    return {
      header: false,
      drawer: false,
      t: false,
      cdmactive: false,
      cddac: false,
      lanActive: false,
    }
  },
  methods: {
    Toggle() {
      this.drawer = !this.drawer
    },
    dropClick() {
      this.cdmactive = !this.cdmactive
      this.cddac = !this.cddac
    },
    langBtn() {
      this.lanActive = !this.lanActive
    },
    langBtnRemove() {
      this.lanActive = false
    },
  },
  mounted() {
    window.addEventListener('scroll', () => {
      if (window.scrollY > 50) {
        this.header = true
      } else {
        this.header = false
      }
    })
  },
}
</script>

<style scoped>
.header_in {
  padding: 0 20px;
  margin: 0 auto;
}
.menu_btn {
  margin: 15px 0;
}
.header_in {
  margin: 0 auto !important;
}
.v-btn:not(.v-btn--round).v-size--default[data-v-61dd7a3d] {
  height: 0px !important;
  min-width: 0px !important;
  padding: 0 0px !important;
  background-color: transparent;
}
.v-btn:not(.v-btn--round).v-size--default[data-v-61dd7a3d] {
  height: 0px !important;
  min-width: 0px !important;
  padding: 20px 20px !important;
  background-color: transparent;
}
.header {
  position: fixed;
  width: 100%;
  top: 0;
  left: 0;
  z-index: 3;
  background-color: transparent;
  transition: 0.5s ease all;
}
a {
  text-decoration: none;
}
.header-active {
  background: #12232e;
}
.img-logo {
  position: absolute;
  width: 100%;
  top: 0;
  left: 0;
  transform: translateX(50deg);
  display: flex;
  align-items: center;
  justify-content: center;
}
.img-logo .relative {
  padding: 20px 10px 20px 20px;
  background: transparent;
  width: 150px;
  height: 150px;
  position: relative;
  border-radius: 50%;
  transition: 0.5s ease all;
}
.img-logo-active {
  width: 130px !important;
  height: 130px !important;
  background: #12232e !important;
}
.drop_menu {
  position: relative;
  z-index: 3;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 191px;
  height: 50px;
  border: 3px solid #007cc7;
  margin: 15px 0;
  border-radius: 30px;
  font-family: 'Montserrat';
  font-weight: 600;
  letter-spacing: 1px;
  cursor: pointer;
  transition: all 0.3s ease-in;
}

.drop_menu:hover {
  background: #007cc7;
}
.drop_menu i {
  margin-right: 6px;
  transition: all 0.4s ease-in;
}
.drop_menu span {
  font-size: 18px;
  margin-left: 6px;
}
.drop_menu:hover i {
  transform: translateX(-12px);
}

.clickdropmenu {
  border-bottom-left-radius: 0px;
  border-bottom-right-radius: 0px;
  border: none;
  background: #007cc7;
}
.drop_down {
  display: none;
  position: absolute;
  bottom: -90px;
  left: 0;
  width: 100%;
  padding: 0;
  background: #007cc7;
  border-bottom-left-radius: 30px;
  border-bottom-right-radius: 30px;
  overflow: hidden;
}

.drop_down li {
  list-style-type: none;
  color: #fff;
  height: 30px;
  font-size: 14px;
  display: flex;
  align-items: center;
  padding-left: 21px;
}
.drop_down li:hover {
  background: #fff;
}
.drop_link {
  color: #fff;
}
.drop_down li:hover .drop_link {
  color: #007cc7;
}

.dropDownActive {
  display: block;
}
/* Lang btn */
.lang_cover {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 4;
  display: none;
}
.lang_btn {
  margin-top: 20px;
  width: 98px;
  height: 45px;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer !important;
  color: #fff;
  z-index: 5;
  transition: all 0.4s ease;
  border-radius: 5px;
}
.lang_btn span {
  text-transform: uppercase;
}
.lang_down {
  position: absolute;
  top: 45px;
  left: 0;
  width: 100%;
  display: none;
  padding: 0;
  text-align: center;
  border-radius: 5px;
}
.lang_down li {
  width: 100%;
  height: 45px;
  background: black;
  color: #fff;
  list-style-type: none;
  padding: 10px 0;
  cursor: pointer;
}

.lang_btn:hover {
  background: rgba(0, 0, 0, 0.2);
}
.lang_active {
  display: block;
}
/* Lang btn end */
.links {
  position: relative;
  z-index: 3;
}
.link {
  text-decoration: none;
  color: white;
  font-size: 20px;
  transition: 0.5s ease all;
}
.close_menu {
  margin-right: 15px;
}
.linkmobile {
  padding: 15px;
  color: white;
  font-size: 17px !important;
}
.link:not(:last-child) {
  margin-right: 50px;
}
.link:hover {
  color: #007cc7;
}
* {
  margin: 0;
  padding: 0;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}
#shop_item {
  color: #eefbfb !important;
  border: 3px solid #007cc7 !important;
  border-radius: 30px;
  padding: 20px 18px !important;
  -webkit-transition: ease 0.5s !important;
  transition: ease 0.5s !important;
  background-color: none;
  width: 171px !important;
}
.shop-click {
  border: 3px solid #007cc7 !important;
  border-radius: 30px 30px 0 0 !important;
  background: #007cc7 !important;
}
#shop_item i {
  -webkit-transition: ease 0.5s !important;
  transition: ease 0.5s;
  margin-right: 15px;
  margin-top: 2px;
  font-size: 20px;
}

#shop_item:hover {
  background-color: #007cc7;
}

#shop_item:hover i {
  -webkit-transform: translateX(-5px);
  transform: translateX(-5px);
}
.v-btn:not(.v-btn--round).v-size--default {
  height: 47px;
  min-width: 100px;
  background-color: transparent;
}
.contacts {
  padding: 10px 20px;
  font-size: 18px;
  -webkit-transition: ease 0.5s;
  transition: ease 0.5s;
  cursor: pointer;
}
.contacts a {
  color: #eefbfb;
  border: 3px solid #007cc7;
  border-radius: 30px;
  padding: 7px 18px;
  -webkit-transition: ease 0.5s;
  transition: ease 0.5s;
}
.contacts a i {
  margin-right: 18px;
  -webkit-transition: ease 0.5s;
  transition: ease 0.5s;
  -webkit-transform: rotate(135deg);
  transform: rotate(135deg);
}

.contacts:hover a {
  background-color: #007cc7;
}

.contacts:hover i {
  -webkit-transform: rotate(0deg);
  transform: rotate(0deg);
}
.mdi-close::before {
  content: '\F0156';
  margin-right: 5px !important;
}
.v-list--dense .v-list-item .v-list-item__title,
.v-list--dense .v-list-item .v-list-item__subtitle {
  font-size: 0.8125rem;
  font-weight: 500;
  font-size: 20px;
  margin: 10px 15px;
  margin: 1;
}
@media (max-width: 650px) {
  .header_in {
    padding: 0 10px;
  }
  .link {
    font-size: 16px;
  }
  .drop_menu {
    width: 150px;
    height: 50px;
  }
  .img-logo .relative {
    width: 100px;
    height: 100px;
  }
  .img-logo-active {
    width: 80px !important;
    height: 80px !important;
    background: #12232e !important;
  }
}
</style>
