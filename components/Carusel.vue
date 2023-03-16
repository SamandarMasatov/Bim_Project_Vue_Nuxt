<template>
  <div class="carusel">
    <div class="btn-group">
      <button @click="changeImg(false)" class="btn btn-left">
        <v-icon color="black">mdi-chevron-left</v-icon>
      </button>
      <button @click="changeImg(true)" class="btn btn-left">
        <v-icon color="black">mdi-chevron-right</v-icon>
      </button>
    </div>
    <NuxtLink :to="`/${$i18n.locale}/${url}/${id}`">
      <v-img
        width="100%"
        height="100%"
        elevation="0"
        class="img"
        :src="`http://api.bimproject.uz/uploads/${name}/${img[i]}`"
      ></v-img>
    </NuxtLink>
  </div>
</template>

<script>
export default {
  props: ['Model', 'img', 'name', 'url', 'id'],
  data() {
    return {
      i: 0,
    }
  },
  methods: {
    changeImg(t) {
      if (t) {
        if (this.Model.length > this.i) {
          this.i++
          console.log(this.Model)
        }
      } else {
        if (this.i > 0) {
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
.btn-group {
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
.btn {
  background: rgba(255, 255, 255, 0.694);
  color: black;
  width: 40px !important;
  height: 40px !important;
  border-radius: 50%;
  outline: none;
  transition: 0.5s ease all;
}
.btn:hover {
  background: rgba(255, 255, 255, 0.854);
}
.btn:active {
  background: rgba(182, 182, 182, 0.694);
}
</style>
