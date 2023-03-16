<template>
  <v-app class="app-model" style="background-color: #12232e">
    <StaHeader />
    <div>
      <StaProjectHeader />

      <div id="rang" class="px-10 mb-15">
        <div style="margin-bottom: 30px" class="pt-10">
          <v-row style="background: #007cc7" class="pa-0">
            <v-col cols="7" class="images pa-0">
              <!-- <div>{{ project }}</div> -->
              <div class="carusel">
                <div class="btn-group">
                  <button
                    @click="changeImg(false)"
                    class="btn btn-left"
                    style="
                      width: 60px !important;
                      height: 60px !important;
                      background: rgba(255, 255, 255, 0.772);
                    "
                  >
                    <v-icon size="40" color="black">mdi-chevron-left</v-icon>
                  </button>
                  <button
                    @click="changeImg(true)"
                    class="btn btn-left"
                    style="
                      width: 60px !important;
                      height: 60px !important;
                      background: rgba(255, 255, 255, 0.772);
                    "
                  >
                    <v-icon size="40" color="black">mdi-chevron-right</v-icon>
                  </button>
                </div>
                <v-img
                  width="100%"
                  height="100%"
                  elevation="0"
                  class="img"
                  @click="showImg(image[it])"
                  :src="`http://api.bimproject.uz/uploads/fprojects/${image[it]}`"
                ></v-img>
              </div>
              <!-- <v-carousel class="pa-0 carousel">
                <v-carousel-item
                  v-for="(item1, i) in project.file"
                  :key="i"
                  @click="showImg(item1)"
                  :src="`http://api.bimproject.uz/uploads/fprojects/${item1}`"
                  class="pa-0"
                ></v-carousel-item>
              </v-carousel> -->
            </v-col>
            <v-col cols="5" style="padding-left: 47px">
              <v-container>
                <h1 class="h1">{{ name }}</h1>
                <table class="table">
                  <tr>
                    <td class="name">{{ $t('maydon') }} :</td>
                    <td class="value">
                      {{ project.space }} м<sup style="font-size: 12px">2</sup>
                    </td>
                  </tr>
                  <tr>
                    <td class="name">{{ $t('xona') }} :</td>
                    <td class="value">{{ project.xona }}</td>
                  </tr>
                  <tr>
                    <td class="name">{{ $t('etaj') }} :</td>
                    <td class="value">{{ project.etaj }}</td>
                  </tr>
                </table>
                <v-btn
                  class="d-flex justify-space-between"
                  width="250"
                  elevation="0"
                  id="download"
                  style="border: 2px solid #fff"
                  :to="`/${$i18n.locale}/Project/pay/${project._id}`"
                >
                  <span>{{ $t('purchase') }}</span> <span>$ {{ project.price }}</span></v-btn
                >
              </v-container>
            </v-col>
          </v-row>
          <v-row class="mt-12" justify="center">
            <v-col cols="12" md="6" v-for="qavat in project.qavat" :key="qavat">
              <div class="floor-name ma-5">{{ qavat.name[$i18n.locale] }}</div>
              <v-simple-table
                style="background: transparent !important"
                class="ma-5"
              >
                <template v-slot:default>
                  <thead>
                    <tr>
                      <th class="text-left">№</th>
                      <th class="text-left">{{ $t('xonaNomi') }}</th>
                      <th class="text-left">{{ $t('maydon') }} m²</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="(xona, index) in qavat.xonalar" :key="index">
                      <td class="text-center">{{ index + 1 }}</td>
                      <td>{{ xona.name[$i18n.locale] }}</td>
                      <td class="text-center">{{ xona.space }}</td>
                    </tr>
                  </tbody>
                </template>
              </v-simple-table>
            </v-col>
          </v-row>
        </div>
      </div>
      <div class="show-img" :class="modal ? 'show-active' : ''">
        <img :src="img" />
        <v-icon @click="modal = true" class="close">mdi-close</v-icon>
      </div>
    </div>
    <StaFooter />
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      id: String(this.$route.params.id),
      i: 0,
      project: [],
      name: '',
      xisob: 1,
      modal: true,
      img: '',
      run: 'Hello worldr',
      image: [],
      it: 0,
    }
  },
  created() {
    this.$axios
      .get('/fprojects/hammasi')
      .then((res) => {
        res.data.forEach((element) => {
          if (element._id == this.id) {
            this.project = element
            this.image = element.file
            this.name = element.name[this.$i18n.locale]
          }
        })
      })
      .catch((err) => {
        this.project = err
      })
  },
  methods: {
    changeImg(t) {
      if (t) {
        if (this.image.length > this.it) {
          this.it++
          console.log(this.image)
        }
      } else {
        if (this.it > 0) {
          this.it--
        }
      }
    },
    showImg(i) {
      this.img = `http://api.bimproject.uz/uploads/fprojects/${i}`
      this.modal = false
    },
    hisobla(id) {
      if (id == 0) {
        this.xisob = 1
      } else {
        this.xisob++
      }
      return this.xisob
    },
    changeImage(direction) {
      if (direction == 'right') {
        if (this.i == this.project.file.length - 1) {
          this.i = 0
        } else {
          this.i++
        }
      } else if (direction == 'left') {
        if (this.i == 0) {
          this.i = this.project.file.length - 1
        } else {
          this.i--
        }
      }
    },
  },
}
</script>

<style scoped>
.carusel {
  width: 100%;
  height: 100%;
  position: relative;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  overflow: hidden;
  transition: 0.5s ease all;
}
.carusel.btn-group {
  transition: 0.5s ease all;
  position: absolute;
  left: -25%;
  top: 50%;
  transform: translateY(-50%);
  background: transparent !important;
  width: 150%;
  height: auto;
  z-index: 2;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.carusel:hover .btn-group {
  width: 100%;
  left: 0;
}
.carusel.btn {
  background: rgba(255, 255, 255, 0.772) !important;
  color: black;
  width: 50px !important;
  height: 50px !important;
  border-radius: 50%;
  outline: none;
  transition: 0.5s ease all;
  padding: 15px;
}
.carusel.btn:hover {
  background: rgba(255, 255, 255, 0.938);
}
.carusel.btn:active {
  background: rgba(168, 168, 168, 0.753);
}
.app-model {
  width: 1300px !important;
  margin: 0 auto;
}
@media (min-width: 1300px) {
  .app-model {
    width: 100% !important;
  }
}
#rang {
  width: 1185px;
  margin: 0 auto;
  background: #203647 !important;
}

@media (min-width: 1264px) {
  #rang {
    margin-bottom: 60px;
  }
}
.v-application--is-ltr .pe-10 {
  padding-right: 0px !important;
}
/* Carousel btn */
.v-window__prev,
.v-window__next {
  background: red !;
}
.show-img {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 20;
  background: rgba(0, 0, 0, 0.89);
}
.show-active {
  display: none;
}
.show-img img {
  height: 90%;
}
.show-img .close {
  position: absolute;
  top: 8%;
  right: 8%;
  font-size: 30px;
  padding: 10px;
  background: #007cc7;
  border-radius: 50%;
}
.text-left {
  background: #12232e;
  border-radius: 20px;
  text-align: center !important;
  font-family: 'Montserrat' !important;
  font-style: normal;
  font-weight: 600;
  font-size: 16px !important;
  line-height: 30px;
  color: #ffffff;
}
#download {
  border-radius: 20px;
  background: transparent !important;
  border: 2px solid #007cc7;
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 30px;
  color: #ffffff;
  padding: 0 30px;
  margin: 0;
}
.images {
  position: relative;
  overflow: hidden;
}
.images .btn-group {
  position: absolute;
  z-index: 2;
  width: 100%;
  top: 50%;
  left: 0;
  transform: translateY(-50%);
  padding: 10px 15px;
  color: black;
  display: flex;
  align-content: center;
  justify-content: space-between;
}
.images .btn-group button {
  background: rgba(255, 255, 255, 0.441);
  outline: none;
  border: none;
  border-radius: 50%;
  transition: 0.5s ease all;
}
.images .btn-group button:hover {
  background: white;
}
.images .btn-group .icon {
  color: black;
  font-size: 55px;
}

.h1 {
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 600;
  font-size: 25px;
  line-height: 24px;
  color: #ffffff;
  margin-top: 84px;
  margin-bottom: 50px;
}
.table .name {
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 500;
  font-size: 20px;
  line-height: 18px;
  padding-bottom: 25px;
  color: #fff;
}
.table .value {
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 500;
  font-size: 20px;
  line-height: 18px;
  padding-left: 54px;
  color: #ffffff;
  padding-bottom: 25px;
}

.floors {
  margin-top: 50px;
}
.floors .floor {
  width: 200px;
  display: inline-flex;
  margin-right: 47px;
  text-align: center;
}
.floors .floor .div {
  width: 100%;
}
.floor-name {
  width: 150px;
  background: #007cc7;
  color: white;
  padding: 10px 10px !important;
  border-radius: 20px;
  text-align: center;
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 500;
  font-size: 20px;
  line-height: 18px;
  margin-bottom: 25px;
  color: #ffffff;
}
.floors .floor .value {
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 500;
  font-size: 17px;
  line-height: 15px;
  margin-bottom: 15px;
}
</style>
