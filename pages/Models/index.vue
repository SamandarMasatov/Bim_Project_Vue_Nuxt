<template>
  <v-app class="app-model" style="background-color: #12232e">
    <StaHeader />
    <div class="mobile">
      <div class="mt-2">
        <div style="padding-top: 80px !important">
          <div
            class="mt-15 px-6 pt-10 ps-10 mobile"
            style="background: #203647"
          >
            <v-row>
              <v-col cols="4">
                <NuxtLink
                  :to="`/${$i18n.locale}/models`"
                  class="text-decoration-none white--text"
                  style="font-size: 40px"
                >
                  {{ $t('dModel') }}
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
                  <div class="search float-right">
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
          class="py-10 mb-15 pb-15"
          style="padding-bottom: 140px !important; background: #203647"
        >
          <v-row>
            <!-- Start model menu page -->
            <v-col cols="3" class="ps-10">
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
                      style="margin: 0"
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
            </v-col>
            <!-- End model menu page -->

            <!-- Start models page -->
            <v-col cols="9">
              <v-row style="box-sizing: border-box !important">
                <v-container style="box-sizing: border-box !important">
                  <div
                    class="models_wrapper"
                    style="box-sizing: border-box !important"
                  >
                    <div
                      class="card_model"
                      v-for="(model, index) of models"
                      :key="index"
                      style="box-sizing: border-box !important"
                    >
                      <v-card
                        @mouseenter="showHover"
                        @mousemove="hoverImg = model.file[imageId]"
                        @mouseleave="hideHover"
                        dark
                        style="background: #007cc7 !important"
                      >
                        <div class="carusel" style="height: 210px">
                          <button class="button btn-left">
                            <v-icon
                              color="white"
                              size="35px"
                              @click="nextPrev(0, model._id)"
                              @mousemove="modId = model._id"
                              @mouseleave="modId = 0"
                              >mdi-chevron-left</v-icon
                            >
                          </button>
                          <button class="button btn-right">
                            <v-icon
                              color="white"
                              size="35px"
                              @click="nextPrev(1, model._id)"
                              @mousemove="modId = model._id"
                              @mouseleave="modId = 0"
                              >mdi-chevron-right</v-icon
                            >
                          </button>
                          <NuxtLink
                            :to="`/${$i18n.locale}/models/${model._id}`"
                          >
                            <div class="bg-model"></div>
                            <v-img
                              :src="`http://api.bimproject.uz/uploads/model/${model.file[0]}`"
                              height="100%"
                              @mousemove="modId = model._id"
                              @mouseleave="modId = 0"
                            ></v-img>
                          </NuxtLink>
                          <div class="btn-group" @mousemove="modId = model._id">
                            <button
                              @mousemove="modId = model._id"
                              v-for="(item, i) in model.file"
                              :key="i"
                              @click="imgId(i, model._id)"
                              :class="model._id == modId ? 'box-shadow' : ''"
                            >
                              <span
                                :class="i == imageId ? 'span-active' : ''"
                              ></span>
                            </button>
                          </div>
                        </div>
                        <v-card-title class="py-1">
                          <NuxtLInk
                            :to="`/${$i18n.locale}/models/${model._id}`"
                            class="text-decoration-none white--text hover"
                            style="
                              font-family: 'Montserrat';
                              font-style: normal;
                              font-weight: 400;
                            "
                          >
                            {{ model.name[$i18n.locale] }} 
                          </NuxtLInk>
                        </v-card-title>

                        <v-card-actions class="px-4">
                          <sapn
                            style="
                              font-size: 16px;
                              font-family: 'Montserrat';
                              font-style: normal;
                              font-weight: 600;
                            "
                            >Pro</sapn
                          >
                          <v-spacer></v-spacer>
                          <v-btn
                            outlined
                            rounded
                            class="white--text"
                            style="
                              font-family: 'Montserrat';
                              font-style: normal;
                              font-weight: 600;
                            "
                            >${{ model.price }}</v-btn
                          >
                        </v-card-actions>
                      </v-card>
                    </div>
                  </div>
                </v-container>
              </v-row>
            </v-col>
            <!-- End models page -->
          </v-row>
          <div class="hoverEffect">
            <v-img
              width="100%"
              height="100%"
              :src="`http://api.bimproject.uz/uploads/model/${hoverImg}`"
            ></v-img>
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
    title: '3d model',
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
      imageId: 0,
      modId: 0,
      hover: true,
      tagWidth: 0,
      right: 0,
      hoverImg: '',
      halfWidth: 0,
      clientWidth: 0,
      layerX: 0,
      arifmeticWidth: 0,
      newModel: [1],
      t: false,
      inputText: '',
      number: [],
      num: '',
    }
  },
  methods: {
    getItems() {
      this.$axios
        .get('/model/allType')
        .then((res) => {
          this.items = res.data
        })
        .catch((err) => {
          console.log(err)
        })
    },
    getItems2() {
      this.$axios
        .get('/model/allType')
        .then((res) => {
          this.items2 = res.data
        })
        .catch((err) => {
          console.log(err)
        })
    },
    getModel() {
      this.$axios
        .get('/model/all')
        .then((res) => {
          this.models = res.data
        })
        .catch((err) => {
          console.log(err)
        })
    },
    getModel2() {
      this.$axios
        .get('/model/all')
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
                this.models2[a].modelType_ID == this.items[i].items[b].id
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

    showHover: function (event) {
      const element = event.srcElement
      const vidth = event.view.innerWidth / 2
      const hoverEffect = document.querySelector('.hoverEffect')
      if (this.hover) {
        this.imageId = 0
        this.tagWidth = event.clientX - event.offsetX
        this.halfWidth = event.clientX
        this.layerX = event.layerX
        this.arifmeticWidth = this.halfWidth - this.layerX
        this.clientWidth = element.clientWidth
        this.hover = false
        if (vidth < this.arifmeticWidth + this.clientWidth / 2) {
          this.right = vidth * 2 - this.tagWidth + 10
          hoverEffect.style.left = 'auto'
          hoverEffect.style.right = `${this.right}px`
        } else {
          this.right = this.tagWidth + this.clientWidth + 15
          hoverEffect.style.right = 'auto'
          hoverEffect.style.left = `${this.right}px`
        }
      } else {
      }
      this.num = setTimeout(() => {
        hoverEffect.classList.add('hoverEffect-active')
      }, 1500)
    },
    hideHover: function (event) {
      this.hover = true
      const hoverEffect = document.querySelector('.hoverEffect')
      hoverEffect.classList.remove('hoverEffect-active')
      this.modId = 0
      clearTimeout(this.num)
    },
    imgId(id, modelId) {
      this.findModel(modelId)
      this.hoverImg = this.newModel.file[id]
      this.imageId = id
    },
    nextPrev(i, modelId) {
      this.findModel(modelId)
      if (i === 1) {
        if (this.newModel.file.length - 1 === this.imageId) {
          this.imageId = 0
        } else {
          this.imageId++
        }
        this.hoverImg = this.newModel.file[this.imageId]
      } else {
        if (this.imageId === 0) {
          this.imageId = this.newModel.file.length - 1
        } else {
          this.imageId--
        }
        this.hoverImg = this.newModel.file[this.imageId]
      }
    },
    findModel(modelId) {
      for (let i = 0; i < this.models.length; i++) {
        if (this.models[i]._id == modelId) {
          this.newModel = this.models[i]
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
@media (min-width: 1300px) {
  .app-model {
    width: 100% !important;
  }
}
.mobile {
  width: 1300px;
  margin: 0 auto;
}
.models_wrapper {
  display: flex !important;
  justify-content: center !important;
  flex-wrap: wrap !important;
}
.card_model {
  margin: 8px 8px;
  width: 215px !important;
  max-height: 500px !important;
}
.font {
  font-family: 'Montserrat';
  font-size: 19px;
  font-weight: 500;
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
  top: 50%;
  transform: translateY(-50%);
  z-index: 100;
  border-radius: 20px;
  overflow: hidden;
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
  z-index: 5;
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
  z-index: 5;
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
/* .carusel .btn-group .box-shadow{
} */
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
/* .btn-group .box-shadow .span-active{
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: white;
} */
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

* {
  box-sizing: border-box !important;
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
.checkbox {
  margin-left: 40px !important;
  margin-bottom: -17px !important;
}
.hoverEffect {
  width: 420px;
  height: 465px;
  border: 3px solid #007cc7;
  transition: 1s ease-in-out;
  /* opacity: 0;
  visibility: hidden; */
  display: none;
}
.hoverEffect-active {
  /* opacity: 1;  */
  display: block;
}
* {
  box-sizing: border-box !important;
}
.datas {
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
.datas-active {
  padding: 20px 30px;
  height: 300px;
  overflow-y: scroll;
}
.datas .link {
  padding: 0;
  color: white;
  text-decoration: none;
  background: red;
}

.datas .link p {
  padding: 0;
  margin: 0;
}
.datas .link .model-name {
  font-size: 22px;
  text-decoration: underline;
}

.datas .link .model-lan {
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
@media (max-width: 600px) {
  .btn-group {
    width: 100%;
    display: flex;
    justify-content: space-between;
  }
}
@media (max-width: 400px) {
  .datas {
    margin-top: 47px;
  }
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
.datas-close {
  background: transparent !important;
  position: absolute;
  top: 5px;
  right: 0px;
}
.bg-model {
  position: absolute;
  width: 100%;
  height: 100%;
  background: transparent;
  z-index: 1;
  transition: 0.3s ease all;
}
.carusel:hover .bg-model {
  background: rgba(0, 0, 0, 0.582);
}
/* @media (max-width: 1265px){
  .mobile{
    background: red;
  }
} */
</style>
