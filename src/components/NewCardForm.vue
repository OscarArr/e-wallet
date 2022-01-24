<template>
  <form @submit.prevent="pushNewCard" @input="cardPreview"> 
    <input class="num" label="CARD NUMBER" 
    placeholder="XXXX XXXX XXXX XXXX"
    type="text" maxlength="19" 
    @input="numberSpacer" 
    v-model="newCard.cardNumber">
    <input class="name" label="CARDHOLDER NAME" 
    placeholder="FIRSTNAME SURNAME" maxlength="20"
    v-model="newCard.cardHolder">
    <div class="expire-date">
      <select v-model="newCard.expireMonth">
        <option value="" disabled>MM</option>
        <option 
        :value="month"
        v-for="month in 12" :key="month">
          {{month}}
        </option>
      </select>
      <select v-model="newCard.expireYear">
        <option value="" disabled>YY</option>
        <option :value="year+2021"
        v-for="year in 5" :key="year">
          {{year+2021}}
        </option>
      </select>
    </div>
  <input class="ccv" type="number" 
  maxlength="3"
  v-model="newCard.CCV">
  <select class="vendor" placholder="CARD VENDOR"
  v-model="newCard.vendor">
    <option value="bitcoin">BITCOIN</option>
    <option value="blockchain">BLOCK CHAIN</option>
    <option value="evil">EVIL CORP</option>
    <option value="ninja">NINJA BANK</option>
  </select>
  <div class="submit">
    <p class="error">{{errorMessage}}</p>
    <button>ADD CARD</button>
  </div>
</form>
</template>

<script>
export default {
  beforeMount(){
    const blankCard = {
      vendor: 'empty',
      cardNumber: 'XXXX XXXX XXXX XXXX',
      cardHolder: 'NNNNN NNNNNNN',
      expireMonth: 'MM',
      expireYear: 'YY',
      CCV: '000'
    }
    this.$emit('updateCard', blankCard)
  },
  data(){return{
    newCard:{
      vendor: '',
      cardNumber: '',
      cardHolder: '',
      expireMonth: '',
      expireYear: '',
      CCV: ''
    },
    errorMessage: ""
  }},
  methods: {
    cardPreview(){
      this.$emit('updateCard', this.newCard)
    },
    pushNewCard(){
        //   if (this.cards.find((number) => number.cardNumber == this.newCard.cardNumber)){
        //     this.errorMessage ='Detta kort finns redan i din e-wallet!'
        //   } else 
      if (this.newCard.vendor == ''){
            this.errorMessage = 'Vänligen välj en bank'
          } else if (this.newCard.expireYear == ''){
            this.errorMessage = 'Vänligen fyll i giltighetsår'
          } else if (this.newCard.expireMonth == ''){
            this.errorMessage = 'Vänligen fyll i giltighetsmånad'
          } else if (this.newCard.cardHolder == ''){
            this.errorMessage = 'Vänligen fyll i namn'
          } else {
            this.errorMessage = ""
            this.$emit('send', {...this.newCard})
          }
        },
    numberSpacer(){
      
    }
  }
}
</script>

<style scoped>
form{
  height: 40vh;
}

</style>