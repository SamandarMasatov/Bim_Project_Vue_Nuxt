<template>
  <div style="padding-top: 80px;!important">
    <v-container class="mt-15 px-6 pt-10" style="background: #203647">
      <v-row>
        <v-col cols="12" sm="5" lg="4">
          <NuxtLink
            :to="`/${$i18n.locale}/Constraction`"
            class="text-decoration-none white--text"
            style="font-size: 40px"
            >{{ $t('konstruksiya') }}</NuxtLink
          >
        </v-col>
        <v-col cols="12" sm="7" lg="4">
          <div class="btn-group float-right" style="text-align: center">
            <button class="btn mr-10">{{ $t('yangi') }}</button>
            <button class="btn">{{ $t('top') }}</button>
          </div>
        </v-col>
        <v-col cols="12" xs="12" lg="4">
          <div style="position: relative">
            <div class="search float-right" :class="t ? 'search-active' : ''">
              <input
                type="text"
                v-model="inputText"
                v-on:keyup.enter="Search()"
              />
              <button @click="Search()">
                <v-icon size="30px" color="white">mdi-magnify</v-icon>
              </button>
            </div>
            <div class="datas" :class="t ? 'datas-active' : ''">
              <div
                class="no-data"
                :class="newModel.length == 0 ? '' : 'd-none'"
              >
                {{ $t('noResult') }}
              </div>
              <div class="data" v-for="(item, i) in newModel" :key="i">
                <NuxtLink
                  :to="`/${$i18n.locale}/Constraction/${item.id}`"
                  class="link my-3"
                >
                  <p class="model-name">{{ item.name }}</p>
                  <p class="model-lan">{{ $t('qidirish') }} {{ item.lan }}</p>
                  <br />
                </NuxtLink>
              </div>
            </div>
          </div>
        </v-col>
      </v-row>
      <div></div>
    </v-container>
  </div>
</template>
<script>
export default {
  data: () => {
    return {
      models: [],
      newModel: [],
      inputText: '',
      t: false,
    }
  },
  created() {
    this.$axios
      .get('/cons/all')
      .then((res) => {
        this.models = res.data
      })
      .catch((err) => {
        console.log(err)
      })
  },
  methods: {
    Search() {
      if (this.inputText.length > 0) {
        this.newModel = []
        this.t = true
        const model = this.models
        model.forEach((item) => {
          if (
            String(item.name.ru).toLocaleLowerCase().search(this.inputText) !=
            -1
          ) {
            this.newModel.push({
              name: item.name.ru,
              lan: 'Russian',
              id: item._id,
            })
          }
          if (
            String(item.name.uz).toLocaleLowerCase().search(this.inputText) !=
            -1
          ) {
            this.newModel.push({
              name: item.name.uz,
              lan: 'Uzbekcha',
              id: item._id,
            })
          }
          if (
            String(item.name.en).toLocaleLowerCase().search(this.inputText) !=
            -1
          ) {
            this.newModel.push({
              name: item.name.en,
              lan: 'English',
              id: item._id,
            })
          }
        })
      } else {
        this.t = false
      }
    },
  },
}
</script>

<style scoped>
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
</style>
