<template>
  <v-app class="app-model" style="background-color: #12232e">
    <StaHeader />
    <div class="mt-2 model-container">
      <div style="padding-top: 80px !important">
        <div class="mt-15 px-6 pt-10 ps-10" style="background: #203647">
          <v-row justify="center">
            <v-col cols="4">
              <NuxtLink
                :to="`/${$i18n.locale}/Project`"
                class="text-decoration-none white--text"
                style="font-size: 40px"
              >
                {{ $t('loyihalar') }}
              </NuxtLink>
            </v-col>
            <v-col cols="4">
              <div class="btn-group float-right" style="text-align: center">
                <button class="btn mr-10">{{ $t('yangi') }}</button>
                <button class="btn">{{ $t('top') }}</button>
              </div>
            </v-col>
            <v-col cols="4">
              <div style="position: relative">
                <div
                  class="search float-right"
                  :class="t ? 'search-active' : ''"
                >
                  <input
                    type="text"
                    v-model="inputText"
                    v-on:keyup.enter="Search()"
                  />
                  <button @click="Search()">
                    <v-icon size="30px" color="white">mdi-magnify</v-icon>
                  </button>
                </div>
              </div>
            </v-col>
          </v-row>
        </div>
      </div>

      <div
        class="py-10 mb-15 pb-15 px-6"
        style="padding-bottom: 140px !important; background: #203647"
      >
        <div class="project_menu_wrapper">
          <!-- Start model menu page -->
          <div class="menu">
            <v-row justify="center">
              <v-expansion-panels accordion>
                <v-expansion-panel
                  v-for="(item, i) in items"
                  :key="i"
                  style="background: #203647 !important"
                >
                  <v-expansion-panel-header>
                    <div class="d-inline-flex">
                      <v-icon class="mr-5">{{ item.action }}</v-icon>
                      <div class="font">{{ item.title[$i18n.locale] }}</div>
                    </div>
                  </v-expansion-panel-header>
                  <v-expansion-panel-content
                    class="pa-0 ma-0"
                    style="margin: 0 !impotant"
                  >
                    <v-checkbox
                      class="pa-0 ma-0 checkbox"
                      v-for="(it, index) in item.items"
                      dark
                      :key="index"
                      :label="it.title[$i18n.locale]"
                      v-model="it.bool"
                      @change="changeItems(i)"
                      style="padding: 0 !important"
                    ></v-checkbox>
                  </v-expansion-panel-content>
                </v-expansion-panel>
              </v-expansion-panels>
            </v-row>
          </div>
          <!-- End model menu page -->

          <div class="project" id="project">
            <div class="project_in">
              <div
                class="project_card"
                v-for="(model, index) in models"
                :key="index"
              >
                <div cols="7" class="pa-0 project_card_img">
                  <!-- Start carousel -->

                  <Carusel
                    :Model="model.file"
                    :img="model.file"
                    :id="model._id"
                    :name="'fprojects'"
                    :url="'Project'"
                    style="height: 100%"
                  />

                  <!-- End carousel -->
                </div>
                <div
                  cols="5"
                  class="project_card_text d-flex flex-column justify-space-between py-3"
                >
                  <div class="title">{{ model.name[$i18n.locale] }}</div>
                  <div class="datas">
                    <div>
                      <span>{{ $t('maydon') }}: </span
                      ><span> {{ model.space }} </span>
                    </div>
                    <div>
                      <span>{{ $t('xona') }}: </span
                      ><span> {{ model.xona }}</span>
                    </div>
                    <div> 
                      <span>{{ $t('etaj') }}: </span
                      ><span> {{ model.etaj }}</span>
                    </div>
                    <div>
                      <span>{{ $t('narx') }}: </span
                      ><span>$ {{ model.price}}</span>
                    </div>
                  </div>
                  <nuxt-link
                    class="kurish pa-0"
                    :to="`/${$i18n.locale}/Project/${model._id}`"
                    elevation="0"
                    >{{ $t('loyiha_kurish') }}</nuxt-link
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <StaFooter />
  </v-app>
</template>

<script>
export default {
  head: {
    title: 'The best architecture finished projects',
    meta: [
      { charset: 'utf-8' },
      { name: 'viewport', content: 'width=device-width, initial-scale=0' },
      {
        hid: 'description',
        name: 'description',
        content: 'my website description',
      },
    ],
    link: [{ rel: 'icon', type: 'image/x-icon', href: '/favicon.ico' }],
  },
  data() {
    return {
      items: this.getItems(),
      items2: this.getItems2(),
      models: this.getModel(),
      models2: this.getModel2(),
      newModel: null,
      projects: [],
      projectAll: [],
      projectName: [],
      projectInfo: [],
      newitem: [],
      newModel: [1],
      t: false,
      inputText: '',
      number: [],
    }
  },
  created() {
    this.$axios
      .get('/ffloor/all')
      .then((res) => {
        this.projectName = res.data
      })
      .catch((err) => {
        console.log(err)
      })
    this.$axios
      .get('/froom/all')
      .then((res) => {
        this.projectInfo = res.data
      })
      .catch((err) => {
        console.log(err)
      })
    this.$axios
      .get('/froom/all')
      .then((res) => {
        this.projects = res.data
      })
      .catch((err) => {
        console.log(err)
      })

    this.$axios
      .get('/ffloor/all')
      .then((res) => {
        this.projectAll = res.data
      })
      .catch((err) => {
        console.log(err)
      })
  },
  methods: {
    getItems() {
      this.$axios
        .get('/fprojects/allType')
        .then((res) => {
          this.items = res.data
          
        })
        .catch((err) => {
          console.log(err)
        })
    },
    getItems2() {
      this.$axios
        .get('/fprojects/allType')
        .then((res) => {
          this.items2 = res.data
        })
        .catch((err) => {
          console.log(err)
        })
    },
    getModel() {
      this.$axios
        .get('/fprojects/hammasi')
        .then((res) => {
          // this.models = res.data
          this.models = res.data
        })
        .catch((err) => {
          console.log(err)
        })
    },
    getModel2() {
      this.$axios
        .get('/fprojects/all')
        .then((res) => {
          this.models2 = res.data
        })
        .catch((err) => {
          console.log(err)
        })
    },
    changeItems(index) {
      for (let i = 0; i < this.items.length; i++) {
        if (index == i) {
          let dat = []
          for (let a = 0; a < this.models2.length; a++) {
            for (let b = 0; b < this.items[i].items.length; b++) {
              if (
                this.items[i].items[b].bool &&
                this.models2[a].ProjectType_ID == this.items[i].items[b].id
              ) {
                dat.push(this.models2[a])
              }
            }
          }
          if (dat.length > 0) {
            this.models = dat
          } else {
            this.models = this.models2
          }
        } else {
          let modelMenu = this.items[i].items
          for (let j = 0; j < modelMenu.length; j++) {
            this.items[i].items[j].bool = false
          }
        }
      }
    },
    Search() {
      if (this.inputText.length > 0) {
        this.t = true
        this.number = []
        const model = this.models2
        model.forEach((item) => {
          // this.number.push(item.name[this.$i18n.locale])
          if (
            String(item.name[this.$i18n.locale])
              .toLocaleLowerCase()
              .search(this.inputText) != -1
          ) {
            this.number.push(item)
          }
        })
        this.models = this.number
      } else {
        this.number = []
        this.models = this.models2
        this.t = false
      }
    },
  },
}
</script>

<style scoped>
.app-model {
  width: 1300px !important;
  margin: 0 auto;
}
.model-container {
  width: 1300px;
  margin: 0 auto;
}

.project_menu_wrapper {
  display: flex;
}
.menu {
  width: 20%;
}
.project {
  width: 80%;
}
.project_in {
  display: flex;
  justify-content: flex-end;
  flex-wrap: wrap;
}
.project_card {
  margin: 15px 5px;
  width: 315px !important;
  height: 200px !important;
  display: flex;
}
.project_card_img {
  width: 60%;
}
.project_card_text {
  padding: 0px 10px;
  width: 40%;
  background: #007cc7;
}
.font {
  font-size: 17px;
  font-weight: 700;
  font-family: 'Montserrat';
}
#project .title {
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 700;
  font-size: 16px !important;
  color: #ffffff;
  margin-bottom: 10px;
}
#project .datas {
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 400;
  font-size: 12px;
  color: #ffffff;
}
#project .kurish {
  border-radius: 20px;
  background: transparent;
  border: 2px solid #fff;
  width: 100%;
  height: 20px;
  box-sizing: border-box;
  margin-top: 10px;
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 400;
  font-size: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 7px 8px;
  text-decoration: none;
  color: #ffffff;
}
.relative {
  position: relative;
}
.models {
  width: 300px;
  position: absolute;
  z-index: 2;
  top: 38px;
  left: -100%;
  transition: 0.5s all ease;
}
.models-active {
  left: 0;
  transition: 0.5s all ease;
}
.hover {
  transition: 0.5s ease all !important;
}
.hover:hover {
  text-decoration: underline !important;
}
.hoverEffect {
  width: 40vw;
  height: 90vh;
  background: white;
  position: fixed;
  bottom: 5vh;
  display: none;
  z-index: 100;
  border-radius: 20px;
  overflow: hidden;
  border: 3px solid #007cc7;
}
.carusel {
  height: 200px;
  width: auto;
  background: #007cc7;
  overflow: hidden;
  position: relative;
}
.carusel .button {
  position: absolute;
  top: 50%;
  transform: translateY(-50deg);
  z-index: 1;
  width: 40px;
  height: 40px;
  background: rgba(0, 0, 0, 0.2);
  border-radius: 50%;
}
.carusel .button:first-child {
  left: -100%;
  transition: 0.5s ease all;
}
.carusel .button:not(:first-child) {
  right: -100%;
  transition: 0.5s ease all;
}
.carusel .btn-group {
  transition: 0.5s ease all;
  width: 100%;
  left: 0;
  bottom: -100%;
  transform: translateY(-100deg);
  position: absolute;
  z-index: 1;
  padding: 0 10%;
  padding-bottom: 10px;
  display: flex;
  justify-content: center;
}
.carusel .btn-group button {
  background: rgba(255, 255, 255, 0.525);
  border-radius: 100px;
  padding: 8px;
  position: relative;
  overflow: hidden;
}

.carusel .btn-group .box-shadow .span-active {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: white;
}
.carusel .btn-group button:not(:last-child) {
  margin-right: 10%;
}
.btn-group .box-shadow {
  background: white;
}

.carusel:hover .btn-group {
  transition: 0.5s ease all;
  bottom: 0;
}
.carusel:hover .btn-left {
  left: 8%;
  transition: 0.5s ease all;
}
.carusel:hover .btn-right {
  right: 8%;
  transition: 0.5s ease all;
}
.rounded {
  border-radius: 10px !important;
  border: 3px solid #007cc7;
  overflow: hidden;
  width: 100% !important;
  box-sizing: border-box !important;
  background: #12232e !important;
}

.search {
  border: 3px solid #007cc7;
  border-radius: 100px;
  display: inline-flex;
  align-items: center;
  padding: 8px 20px;
  width: 100% !important;
}
.search input {
  border: none;
  outline: none;
  font-size: 20px;
  color: white;
  width: 0;
  transition: 0.5s ease all;
  width: 100%;
}
.search button {
  color: white;
  border: none;
  outline: none;
}
.btn {
  padding: 8px 40px !important;
  border: 3px solid #007cc7;
  border-radius: 100px;
  font-size: 20px;
  color: white;
  transition: 0.5s ease all;
}
.btn:hover {
  background: #007cc7;
}

.checkbox {
  margin-left: 40px !important;
  margin-bottom: -17px !important;
}

* {
  box-sizing: border-box !important;
}
.datass {
  position: absolute;
  z-index: 2;
  left: 0;
  width: 100%;
  background: #007cc7;
  margin-top: 51px;
  border-radius: 0 0 0 30px;
  padding: 0 30px;
  height: 0;
  overflow: hidden;
  transition: 0.5s ease all;
}
.datass-active {
  padding: 20px 30px;
  height: 300px;
  overflow-y: scroll;
}
.datass .link {
  padding: 0;
  color: white;
  text-decoration: none;
  background: red;
}

.datass .link p {
  padding: 0;
  margin: 0;
}
.datass .link .model-name {
  font-size: 22px;
  text-decoration: underline;
}

.datass .link .model-lan {
  font-size: 12px;
}

.no-data {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  background: transparent;
  font-size: 25px;
  z-index: 2;
  background: #007cc7;
  display: flex;
  align-items: center;
  justify-content: center;
}
.search {
  border: 3px solid #007cc7;
  border-radius: 30px;
  display: inline-flex;
  align-items: center;
  padding: 8px 20px;
  width: 100% !important;
  transition: 0.5s ease all;
}
.search-active {
  border-radius: 30px 30px 0 0;
}
.search input {
  border: none;
  outline: none;
  font-size: 20px;
  color: white;
  width: 0;
  transition: 0.5s ease all;
  width: 100%;
}
.search button {
  color: white;
  border: none;
  outline: none;
}
.btn {
  padding: 8px 40px !important;
  border: 3px solid #007cc7;
  border-radius: 100px;
  font-size: 20px;
  color: white;
  transition: 0.5s ease all;
}
.btn:hover {
  background: #007cc7;
}
.datas-close {
  background: transparent !important;
  position: absolute;
  top: 5px;
  right: 0px;
}
/* Responsive */
@media (min-width: 1500px) {
  .app-model {
    width: 100% !important;
    margin: 0 auto;
  }
  .model-container {
    width: 1400px;
    margin: 0 auto;
  }
  .project_in {
    justify-content: center;
  }
  /* .project_card {
    margin: 10px 0px;
    width: 337px !important;
    max-height: 300px !important;
  } */
}
@media (min-width: 1300px) {
  .app-model {
    width: 100% !important;
  }
}

@media (min-width: 1264px) {
  .rounded {
    display: none !important;
  }
}
@media (max-width: 1264px) {
  .hoverEffect {
    display: none !important;
  }
}

@media (max-width: 600px) {
  .btn-group {
    width: 100%;
    display: flex;
    justify-content: space-between;
  }
}
@media (max-width: 400px) {
  .search {
    width: 100% !important;
    padding: 6px 20px !important;
  }
  .search input {
    width: 100%;
  }
  .btn-group {
    width: 100%;
    display: flex;
    justify-content: space-between;
  }
  .btn {
    margin: 0 !important;
    font-size: 16px;
    padding: 6px 20px !important;
  }
  .text-decoration-none {
    font-size: 30px !important;
  }
}
</style>
