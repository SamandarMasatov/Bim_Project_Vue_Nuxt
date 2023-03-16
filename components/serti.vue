<template>
  <div class="sertifikats" style="padding-top: 59px">
    <div class="sertificat-title" style="margin-top: 50px">
      <span>{{ $t('sertifikat') }}</span>
    </div>
    <div class="container">
      <div class="p">
        {{ $t('sertiTitle') }}
      </div>

      <v-sheet
        class="mx-auto pa-0 mobil"
        elevation="8"
        width="100%"
        height="400px"
        style="background: transparent !important; box-shadow: none !important"
      >
        <v-slide-group
          v-model="model"
          class="pa-4 mobil"
          show-arrows
          style="height: 100%"
        >
          <v-slide-item v-for="n in images" :key="n">
            <v-card class="ma-4" height="100%" width="250">
              <img
                id="img"
                :src="`http://api.bimproject.uz/uploads/serti/${n.image}`"
                alt=""
              />
            </v-card>
          </v-slide-item>
        </v-slide-group>
      </v-sheet>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      images: [],
    }
  },
  created() {
    this.$axios
      .get('/serti/all')
      .then((res) => {
        this.images = res.data
      })
      .catch((err) => {
        console.log(err)
      })
  },
}
</script>

<style scoped>
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
.title .span {
  position: relative;
  z-index: 2;
  background: #203647;
  padding: 0 10px;
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
.img {
  position: absolute;
  top: 0;
  right: 10%;
  max-width: 550px;
  height: 380px;
  object-fit: cover;
}
@media (max-width: 610px) {
  .sertifikats {
    margin: 0;
    padding: 0;
  }
  .container {
    padding: 40px 0;
  }
  .mobil {
    padding: 0 !important;
    margin: 0 !important;
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
    font-size: 30px;
    line-height: 43px;
    color: #ffffff;
    width: 100%;
    padding-top: 20px;
  }
}
</style>
