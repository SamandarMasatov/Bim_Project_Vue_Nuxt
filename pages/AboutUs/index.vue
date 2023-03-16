<template>
<v-app style="background-color: #12232e">
  <Header/>
  <div>
    <v-carousel
      id="Home"
      cycle
      height="650px"
      show-arrows-on-hover
      hide-delimiters
    >
      <div class="home_wrapper relative">
        <div class="home_text">
          <v-container class="text-left pa-0">
            <h1>{{ $t('biz_haqimizda') }}</h1>
            <p>{{ $t('home_title') }}</p>
          </v-container>
        </div>
        <v-carousel-item v-for="i in imgs" :key="i" style="overflow: hidden">
          <v-img :src="i" height="100%">
            <v-row class="fill-height" align="center" justify="center">
              <div
                class="text-h1 white--text"
                style="
                  width: 100% !important;
                  height: 150vh !important;
                  background-color: rgba(0, 0, 0, 0.6) !important;
                "
              ></div>
            </v-row>
          </v-img>
        </v-carousel-item>
      </div>
    </v-carousel>

    <v-container class="con">
      <v-row style="margin: 100px 0; position: relative">
        <v-col cols="12" md="4">
          <img
            :src="`http://api.bimproject.uz/uploads/about/${img}`"
            class="d-md-none"
            style="width: 100%"
          />
        </v-col>
        <v-col cols="12" md="8" style="background: #203647; position: relative">
          <div class="title my-2 text-right">
            <span class="span me-15">{{ $t('kompHaqida') }}</span>
            <hr class="chiziq" />
          </div>
          <v-row>
            <v-col
              cols="0"
              md="2"
              class="mt-5 md-flex-none"
              style="position: relative"
            >
              <img
                :src="`http://api.bimproject.uz/uploads/about/${img}`"
                class="img d-none d-md-block"
              />
            </v-col>
            <v-col cols="12" md="10">
              <div class="text text-left">
                {{ about }}
              </div>
            </v-col>
          </v-row>
        </v-col>
      </v-row>

      <!-- Start Director page -->
      <v-row class="director">
        <v-col cols="12" sm="6" md="5" lg="5" xl="4">
          <img class="icon" :src="`http://api.bimproject.uz/uploads/teamd/${director.image}`" alt="">
        </v-col>
        <v-col cols="12" sm="6" md="7" lg="7" xl="8" class="text-left dir">
          <div class="name">{{dirName}}</div>
          <div class="name-title">{{positsiya}}</div>
          <div class="p">
            {{desc}}
          </div>
          <div class="icons">
            <a :href="director.facebook">
              <img src="/img/facebook.png" alt="" />
            </a>
            <a :href="director.telegram">
              <img src="/img/telegram.png" alt="" />
            </a>
            <a :href="director.instagram" class="ms-2">
              <img src="/img/instagram.png" alt="" />
            </a>
          </div>
        </v-col>
      </v-row>
      <!-- End Director page -->

      <!-- Start Team page -->
      <v-row class="team" justify="center">
        <v-col
          cols="12"
          sm="6"
          lg="4"
          xl="3"
          class="my-5"
          v-for="(team ,index) in teams"
          :key="index"
        >
          <div class="item">
            <img class="icon" :src="`http://api.bimproject.uz/uploads/team/${team.image}`">
            <div class="data">
              <div class="data-name">{{team.name[$i18n.locale]}} {{team.lastName[$i18n.locale]}}</div>
              <div class="data-title">{{team.position[$i18n.locale]}}</div>
             
            </div>
          </div>
        </v-col>
      </v-row>
      <!-- End Team page -->

      <Serti />

     
    </v-container>
  </div> 
  <Footer/>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      about: '',
      img: '',
      model: null,
      imgs: ['/img/bg1.jpg', '/img/bg2.jpg', '/img/bg3.jpg'],
      teams: [],
      director: [],
      dirName: "",
      positsiya: "",
      desc: "",
    }
  },
  created() {
    this.$axios.get('/teamd/all').then((res) => {
      this.director = res.data[0];
      this.dirName = res.data[0].name[this.$i18n.locale] + " " + res.data[0].lastName[this.$i18n.locale]
      this.positsiya = res.data[0].position[this.$i18n.locale]
      this.desc = res.data[0].description[this.$i18n.locale]
    }).catch((err) => {
      console.log(err);
    })
    this.$axios.get('/team/all').then((res) => {
      this.teams = res.data;
    }).catch((err) => {
      console.log(err);
    })
    this.$axios
      .get('/about/all')
      .then((res) => {
        res.data.forEach((element) => {
          this.about = element.name[this.$i18n.locale]
          this.img = element.image
        })
      })
      .catch((err) => {
        console.log(err)
      })
  },
  mounted() {
    $('.owl-carousel').owlCarousel({
      loop: true,
      margin: 20,
      outoplay: true,
      outoplayTimeout: 3000,
      responsive: {
        0: {
          items: 1,
        },
        600: {
          items: 2,
        },
        1000: {
          items: 3,
        },
      },
    })
  },
  methods: {
    next() {
      document.querySelector('.owl-next').click()
    },
    prev() {
      document.querySelector('.owl-prev').click()
    },
  },
}
</script>

<style scoped>
.team {
  margin: 100px 0;
}
.team .item {
  position: relative;
  width: 250px;
  height: 250px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: white;
  border-radius: 50%;
  overflow: hidden;
  margin: auto;
}
.team .data {
  transition: 0.5s ease all;
  position: absolute;
  bottom: 0;
  left: 0;
  transform: translateY(100%);
  background: #007cc7;
  height: 100%;
  width: 100%;
  padding: 16px;
}
.team .item:hover .data {
  transform: translateY(70%);
}
.team .data .data-name {
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  color: #ffffff;
}
.team .data .data-title {
  margin: 2px 0 8px 0;
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 300;
  font-size: 14px;
  color: #ffffff;
}
.team .data .data-icons a {
  text-decoration: none;
}
.team .data .data-icons a img {
  width: 20px;
  height: 20px;
  object-fit: cover;
}
.team .item .icon {
  width: 100%;
  height: 100%;
  border-radius: 50%;
  position: absolute;
  object-fit: cover;
  left: 0;
}
.director .icons {
  margin-top: 26px;
}
.director .icons a {
  text-decoration: none;
  margin-right: 17px;
}
.director .icon {
  width: 300px;
  height: 300px;
  border-radius: 50%;
}
.director .name {
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 700;
  font-size: 35px;
  line-height: 30px;
  color: #ffffff;
}
.director .name-title {
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 300;
  font-size: 25px;
  line-height: 30px;
  color: #ffffff;
  margin: 20px 0;
}
.director .p {
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 300;
  font-size: 20px;
  line-height: 30px;
  color: #ffffff;
  max-width: 776px;
}
@media (max-width: 600px) {
  .director .dir {
    text-align: center !important;
    margin-top: 20px;
  }
  .director .icon {
    font-size: 200px;
  }
  .team .item {
    width: 200px;
    height: 200px;
  }
  .team .item:hover .data{
    transform: translateY(30%);
  }
}
.home_wrapper {
  width: 100% !important;
  height: 100% !important;
  background-color: rgba(0, 0, 0, 0.59) !important;
}
.home_text {
  display: inline-block;
  background-color: transparent !important;
  position: absolute;
  top: 40% !important;
  color: #fff;
  text-align: left;
  left: 0;
  width: 100%;
  z-index: 1;
  transform: translate(-50deg) !important;
  text-align: left;
}
.home_text h1 {
  position: relative;
  z-index: 1;
  font-size: 80px;
  font-style: normal;
  font-weight: 600;
}
.home_text p {
  position: relative;
  z-index: 1;
  font-size: 25px;
}
@media (max-width: 570px) {
  h1 {
    font-size: 70px !important;
  }
  p {
    font-size: 22px !important;
  }
}
#img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.container {
  width: 100%;
  padding: 40px 50px;
  text-align: center;
}
.sertifikats {
  background: #203647;
  margin-bottom: 60px;
  padding-top: 40px;
}
.sertifikats .sertificat-title {
  width: 100%;
  position: relative;
  height: 5px;
  background: white;
  text-align: center;
  margin-bottom: 40px;
}
.sertifikats .sertificat-title span {
  position: absolute;
  background: #203647;
  color: white;
  transform: translate(-50%, -40%);
  padding: 0 10px;
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 600;
  font-size: 35px;
  line-height: 43px;
  color: #ffffff;
}
.chiziq {
  width: 100%;
  position: absolute;
  top: 40px;
  left: 0;
  z-index: 1;
  height: 5px;
  background: white;
}
.title {
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 600;
  font-size: 35px;
  line-height: 43px;
  color: #ffffff;
}
@media (max-width: 960px) {
  .title {
    text-align: center !important;
  }
  .title span {
    margin-right: 0 !important;
  }
}
.title .span {
  position: relative;
  z-index: 2;
  background: #203647;
  padding: 0 10px;
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 600;
  font-size: 35px;
  line-height: 43px;
  color: #ffffff;
}
.text {
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 400;
  font-size: 15px;
  line-height: 30px;
  color: #ffffff;
  padding: 70px 41px 90px 0 !important;
}
@media (min-width: 1000px) {
  .text {
    height: 400px;
  }
}
.img {
  position: absolute;
  top: 0;
  right: 10%;
  max-width: 550px;
  height: 380px;
  object-fit: cover;
}
@media (max-width: 610px) {
  .con {
    padding: 0 10px;
    margin: 0;
    width: 100%;
  }
}
</style>
