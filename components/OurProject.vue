<template>
  <v-container
    id="Project"
    class="py-4 mt-16 px-0"
    style="background-color: #203647 !important"
  >
    <v-card
      elevation="0"
      class="text-center px-4"
      style="background-color: #203647 !important; padding-top: 59px"
    >
      <h1 class="projecttitle" style="color: #fff; text-decoration: uppercase">
        {{ $t('loyiha') }}
      </h1>
      <p class="projecttext my-12" style="color: #fff">
        {{ $t('loyiha_nomi') }}
        <br />
        <br />
      </p>
    </v-card>

    <v-sheet class="mx-auto m-0 transparent" dark width="100%">
      <v-slide-group
        v-model="model"
        multiple
        show-arrows
        center-active
        style="width: 100% !important"
      >
        <v-slide-item v-for="(data, n) in datas" :key="n" v-slot="{ toggle }">
          <v-card @click="toggle" color="#12232E" class="project_card mx-2">
            <v-row class="row">
              <v-col class="project_wrapper" cols="12" sm="6">
                <nuxt-link :to="`/${$i18n.locale}/Project/${data._id}`">
                  <v-img
                    class="project_img"
                    width="100%"
                    height="100%"
                    style="height: 100% !important"
                    :src="`http://api.bimproject.uz/uploads/fprojects/${data.file[0]}`"
                  ></v-img>
                </nuxt-link>
              </v-col>
              <v-col cols="0" sm="6">
                <div
                  style="
                    margin: 0;
                    width: 100%;
                    height: 100%;
                    box-sizing: border-box !important;
                  "
                  class="cards"
                >
                  <span>
                    <h1 class="cardtitle py-3">
                      {{ data.name[$i18n.locale] }}
                    </h1>
                    <p style="font-weight: 600 !important">
                      {{ $t('maydon') }} :
                      <span
                        style="font-weight: 400 !important; margin-left: 10px"
                        >{{ data['space'] }}</span
                      >
                    </p>
                    <p style="font-weight: 600 !important">
                      {{ $t('xona') }} :
                      <span
                        style="font-weight: 400 !important; margin-left: 10px"
                        >{{ data.xona }}</span
                      >
                    </p>
                    <p style="font-weight: 600 !important">
                      {{ $t('etaj') }} :
                      <span
                        style="font-weight: 400 !important; margin-left: 10px"
                        >{{ data.etaj }}</span
                      >
                    </p>
                    <p style="font-weight: 600 !important">
                      {{ $t('narx') }} :
                      <span
                        style="font-weight: 400 !important; margin-left: 10px"
                        >$ {{ data['price'] }}</span
                      >
                    </p>
                    <v-btn
                      depressed
                      outlined
                      rounded
                      color="#fff"
                      class="button mt-3"
                      :to="`/${$i18n.locale}/Project/${data._id}`"
                      >{{ $t('loyiha_kurish') }}</v-btn
                    >
                  </span>
                </div>
              </v-col>
            </v-row>
          </v-card>
        </v-slide-item>
      </v-slide-group>
    </v-sheet>
    <div style="width: 100% !important; text-align: center">
      <v-container>
        <v-btn
          :to="`/${$i18n.locale}/Project`"
          class="btn my-5 mt-10 px-15"
          outlined
          rounded
          elevation="2"
          >{{ $t('loyihaga_utish') }}</v-btn
        >
      </v-container>
    </div>
  </v-container>
</template>

<script>
export default {
  name: 'OurProjectPage',
  data: () => ({
    model: null,
    datas: [],
  }),
  created() {
    this.$axios
      .get('/fprojects/hammasi')
      .then((res) => {
        this.datas = res.data
      })
      .catch((err) => {
        console.log(err)
      })
  },
}
</script>

<style scoped>
#Project {
  margin: 0 auto !important;
}
.btn {
  padding: 0 100px !important;
  color: #fff !important;
  transition: all 1s ease !important;
  border: 2px solid #007cc7 !important;
}
.btn:hover {
  border: transparent !important;
  color: #fff !important;
  background-color: #007cc7 !important;
}
.projecttitle {
  display: flex !important;
  align-items: center !important;
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 600;
  font-size: 40px;
  line-height: 49px;
}
.projecttext {
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 400;
  font-size: 14px;
  line-height: 30px;
}
.projecttitle:before {
  content: '';
  height: 4px;
  margin-right: 20px !important;
  flex: 1;
  display: block;
  background-color: #fff;
}
.projecttitle:after {
  content: '';
  height: 4px;
  margin-left: 20px !important;
  flex: 1;
  display: block;
  background-color: #fff;
}
.button {
  text-transform: none !important;
  font-weight: 300 !important;
}
.v-application p {
  margin-left: 4px;
  margin-bottom: 4px;
  font-weight: 600;
  font-size: 14px;
}
.v-application .py-4 {
  margin-left: 10px;
  padding-top: 0px !important;
  padding-bottom: 9px !important;
}
.v-btn:not(.v-btn--round).v-size--default {
  /* margin-left: 10px; */
  height: 28px;
  width: 133px;
  padding: 0 16px;
  margin-bottom: 15px;
}
.cardtitle {
  font-size: 18px;
  font-weight: 700;
}
.row {
  max-height: 650px !important;
  width: 400px;
}
@media (max-width: 599px) {
  .v-btn:not(.v-btn--round).v-size--default {
    width: 150px;
  }
  .project_wrapper {
    height: 300px !important;
  }
  .row {
    text-align: center !important;
    /* height: 595px !important; */
    width: 350px !important;
  }
  .row .project_img {
    height: 100% !important;
  }
  .btn {
    width: 70% !important;
    padding: 0 !important;
  }
  .cardtitle {
    font-size: 20px;
  }
}
@media (max-width: 570px) {
  h1 {
    font-size: 22px !important;
  }
  p {
    font-size: 14px !important;
  }
}
@media (max-width: 375px) {
  .row {
    width: 275px !important;
  }
}
</style>
