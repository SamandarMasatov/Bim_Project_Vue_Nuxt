<template>
  <v-app class="app-model" style="background-color: #12232e">
    <StaHeader />
    <div class="mt-12" style="background: #12232e !important">
      <StaConsHeader />
      <div id="rang" class="px-10 py-10 mb-15" style="background: #203647">
        <v-row
          style="background: #007cc7; height: 550px; box-sizing: border-box"
        >
          <v-col cols="6" style="padding: 0; height: 550px">
            <div class="img">
              <v-img
                width="100%"
                height="100%"
                @click="showImg(images[imgId])"
                :src="`http://api.bimproject.uz/uploads/cons/${images[imgId]}`"
              ></v-img>
              <button class="btn" @click="nextPrev(false)">
                <v-icon size="60px" color="white">mdi-chevron-left</v-icon>
              </button>
              <button class="btn" @click="nextPrev(true)">
                <v-icon size="60px" color="white">mdi-chevron-right</v-icon>
              </button>
            </div>
          </v-col>
          <v-col
            cols="6"
            class="margin-bottom"
            style="background: #007cc7; padding: 0 30px 0 40px"
          >
            <div
              class="white--text text-logo mt-8"
              style="
                font-size: 40px;
                margin-top: 20px;
                font-family: 'Montserrat';
                font-style: normal;
                font-weight: 600;
              "
              v-for="(name, i) in model.name"
              :key="i"
            >
              <span v-if="i == $i18n.locale">{{ name }}</span>
            </div>
            <v-btn
              :to="`/${$i18n.locale}/Constraction/pay/${model._id}`"
              outlined
              rounded
              color="white"
              class="btn1 white--text py-8 my-5 d-flex justify-space-around"
              width="100%"
              style="
                font-size: 30px;
                font-family: 'Montserrat';
                font-style: normal;
                font-weight: 600;
              "
            >
              <span>{{ $t('purchase') }}</span>
              <span>${{ model.price }}</span>
            </v-btn>
            <div
              style="background: #007cc7"
              class="mt-5 pt-1 rounded white--text"
            >
              <div
                v-for="(review, index) in reviews"
                :key="index"
                style="
                  font-size: 25px;
                  linear-height: 36px;
                  font-family: 'Montserrat';
                  font-style: normal;
                  font-weight: 400;
                "
                class="my-5 text-item"
              >
                <b
                  class="mr-5"
                  style="
                    font-family: 'Montserrat';
                    font-style: normal;
                    font-weight: 600;
                  "
                  >{{ review.title }}</b
                >
                {{ review.value }}
              </div>
            </div>
          </v-col>
        </v-row>
      </div>
      <div
        class="d-lg-none"
        style="height: 580px; background: transparent"
      ></div>
      <div class="show-img-div" :class="modal ? 'show-active' : ''">
        <img :src="img" class="show-img" />
        <v-icon class="close" @click="modal = true">mdi-close</v-icon>
      </div>
    </div>
    <StaFooter />
  </v-app>
</template>

<script>
export default {
  async asyncData({ params }) {
    const id = await params.id
    return { id }
  },
  data() {
    return {
      Id: null,
      model: [],
      images: [],
      imgId: 0,
      reviews: [],
      img: '',
      modal: true,
    }
  },
  created() {
    this.$axios
      .get('/cons/all')
      .then((res) => {
        let models = res.data
        for (let i = 0; i < models.length; i++) {
          const id = String(this.$route.params.id)
          if (models[i]._id == id) {
            this.model = models[i]
            this.images = models[i].file
            let date = this.model.date
            let fullDate =
              date[0] +
              date[1] +
              date[2] +
              date[3] +
              ' ' +
              date[5] +
              date[6] +
              ' ' +
              date[0] +
              date[1]
            this.reviews = [
              { title: this.$t('razmer'), value: this.model.size + 'mb' },
              { title: this.$t('faylTuri'), value: this.model.fileType },
              { title: this.$t('vaqt'), value: fullDate },
            ]
          }
        }
      })
      .catch((err) => {
        console.log(err)
      })
  },
  methods: {
    showImg(index) {
      this.img = 'http://api.bimproject.uz/uploads/cons/' + index
      this.modal = false
    },
    nextPrev(t) {
      if (t) {
        if (this.imgId >= this.images.length - 1) {
          this.imgId = 0
        } else {
          this.imgId++
        }
      } else if (this.imgId <= 0) {
        this.imgId = this.images.length - 1
      } else {
        this.imgId--
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
.show-img-div {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.874);
  z-index: 20;
  display: flex;
  align-items: center;
  justify-content: center;
}
.show-active {
  display: none;
}
.show-img-div img {
  height: 90%;
}
.show-img-div .close {
  position: absolute;
  top: 8%;
  right: 8%;
  font-size: 30px;
  background: #007cc7;
  border-radius: 50%;
  padding: 10px;
}
.img {
  position: relative !important;
  height: 100%;
}
.btn {
  position: absolute;
  top: 50%;
  transform: translateY(-30%);
  font-size: 30px;
  background: rgba(128, 128, 128, 0.4);
  height: 120px;
  transition: 0.5s ease all;
  border-radius: 0 100px 100px 0;
}
.btn:last-child {
  right: 0;
  border-radius: 100px 0 0 100px;
}
.btn:hover {
  background: rgba(128, 128, 128, 0.7);
}
.imgCards {
  border-radius: 5px;
  transition: 0.5s ease all;
  position: relative;
  z-index: 1;
  overflow: hidden;
  width: 60px;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.imgCards .active {
  width: 100% !important;
  height: 100% !important;
}
.btn1 {
  border-radius: 100px !important;
  border: 3px solid white;
}
.btn1:hover {
  background: #007cc7 !important;
}

@media (max-width: 500px) {
  .text-logo {
    font-size: 30px !important;
  }
  .btn1 {
    font-size: 30px !important;
    padding: 20px 0 !important;
  }
  .text-item {
    font-size: 20px !important;
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
.btn2 {
  padding: 8px 40px !important;
  border: 3px solid #007cc7;
  border-radius: 100px;
  font-size: 20px;
  color: white;
  transition: 0.5s ease all;
}
.btn2:hover {
  background: #007cc7;
}
@media (max-width: 600px) {
  .btn-group2 {
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
  .btn-group2 {
    width: 100%;
    display: flex;
    justify-content: space-between;
  }
  .btn2 {
    margin: 0 !important;
    font-size: 16px;
    padding: 6px 20px !important;
  }
  .text-decoration-none {
    font-size: 30px !important;
  }
}

.model-3d {
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 600;
}
</style>
