<template>
  <div>
    <div class="pay_form_container">
      <div class="close" @click="$emit('closePay', true)">
        <v-icon size="30px" color="white">mdi-close-thick</v-icon>
      </div>

      <h2 class="text-center">{{ Model }} {{ $t('buyProduct') }}</h2>
      <v-row>
        <v-col cols="12" lg="6" class="number_wrapper">
          <label class="number_label ms-3">{{ $t('telNumber') }}</label>
          <input
            type="number"
            class="number"
            placeholder="Telefon raqam yozing"
            v-model="phone"
          />
          <label class="number_label ms-3">978070416</label>
        </v-col>
        <v-col cols="12" lg="6" class="number_wrapper">
          <label class="number_label ms-3">Karta raqam</label>
          <input
            type="number"
            class="number"
            placeholder="Telefon raqam yozing"
            v-model="cardNumber"
          />
          <!-- <label class="number_label">998978070416</label> -->
        </v-col>
        <v-col cols="12" lg="6" class="number_wrapper">
          <label class="number_label ms-3">Ishlab chiqarilgan sanasi</label>
          <input
            type="number"
            class="number"
            placeholder="Telefon raqam yozing"
            v-model="cardExpire"
          />
          <label class="number_label ms-3">08/27</label>
        </v-col>
      </v-row>
      <button @click="sendData" class="btn_pay">To'lash</button>
    
    <!-- code -->
    <div class="confirm">

    </div>
    </div>
    <div class="full_cover" @click="$emit('closePay', true)"></div>
  </div>
</template> 

<script>
export default { 
  props: ['Price', 'Mname', 'Model'],
  data() {
    return {
      close: false,
      payActive: false,
      dollirKurs: '',
      usd: 0,
      some: '',
      phone: '',
      cardNumber: '',
      cardExpire: '',
      personalAccount: 'Samandar',
      price: '100',
    }
  },
  created() {
    this.$axios
      .get('https://nbu.uz/uz/exchange-rates/json/')
      .then((res) => {
        this.dollirKurs = res.data.filter((item) => item.code === 'USD')
        this.usd = this.dollirKurs[0].nbu_buy_price
      })
      .catch((err) => {
        console.log(err)
      })
    // this.$axios.get('/upay/pay').then((res) => {
    //   console.log('XML result', res.data)
    //   this.some = res.data
    // })
  },
  methods: {
    payActive() {
      this.payActive = true
    },
    sendData() {
      this.$axios
        .get('/upay/pay', {
          params: {
            phone: this.phone,
            cardNumber: this.cardNumber,
            cardExpire: this.cardExpire,
            personalAccount: this.personalAccount,
            price: this.price,
          },
        })
        .then((res) => {
          console.log('xml', res.data)
        })
        .catch((err) => {
          console.log(err)
        })
    },
  },
}
</script>

<style scoped>
.full_cover {
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 1;
}
.pay_form_container {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border-radius: 15px;
  width: 700px;
  padding: 20px 20px;
  background: #12232e;
  color: #000;
  z-index: 5;
}
.pay_form_container h2 {
  color: #fff;
}
.close {
  color: #000;
  float: right;
  cursor: pointer;
}
.number_wrapper {
  /* max-width: 400px; */
  margin: 0 auto;
}
.number_label {
  /* text-align: center; */
  display: block;
  color: rgba(255, 255, 255, 0.5);
  margin: 5px 0;
}
.number {
  width: 100%;
  height: 40px;
  margin: 0 auto;
  border: 3px solid #007cc7;
  border-radius: 30px;
  outline: none;
  display: block;
  align-items: center;
  padding: 8px 20px;
  transition: 0.5s ease all;
  color: #fff;
}
.btn_pay {
  display: block;
  margin: 0 auto;
  color: #fff;
  border: 3px solid #007cc7;
  width: 100px;
  height: 40px;
  border-radius: 5px;
  background: #203647;
}
</style>
