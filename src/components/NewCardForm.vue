<template>
  <form @submit.prevent="pushNewCard" @input="cardPreview"> 
	<p>CARD NUMBER</p>
    <input class="num" 
    placeholder="#### #### #### ####"
    type="text" maxlength="16" minlength="16"
    v-model="newCard.cardNumber">
	<p>CARDHOLDER NAME</p>
    <input type="text" class="name"
    placeholder="FIRSTNAME LASTNAME" maxlength="20" 
    v-model="newCard.cardHolder">
    <p class="valid-label">VALID THRU</p>
    <div class="expireDate-CCV">
      <p>month</p>
      <select v-model="newCard.expireMonth">
        <option value="" disabled>MM</option>
        <option 
        :value="month"
        v-for="month in 12" :key="month">
          {{month}}
        </option>
      </select>
      <p>year</p>
      <select v-model="newCard.expireYear">
        <option value="" disabled>YY</option>
        <option :value="year+21"
        v-for="year in 5" :key="year">
          {{year+21}}
        </option>
      </select>
      <p>CCV</p>
      <input class="ccv" type="number" 
      maxlength="3"
      v-model="newCard.CCV">
    </div>
	<p>CARD VENDOR</p>
  <select class="vendor" placholder="CARD VENDOR"
  v-model="newCard.vendor">
    <option value="bitcoin">BITCOIN</option>
    <option value="blockchain">BLOCK CHAIN</option>
    <option value="evil">EVIL CORP</option>
    <option value="ninja">NINJA BANK</option>
  </select>
  <div class="submit">
    <p class="error">{{errorMessage}}</p>
    <button class="add-card-button">ADD CARD</button>
  </div>
</form>
</template>

<script>
export default {
  beforeMount(){
    const blankCard = {
      vendor: 'empty',
      cardNumber: '################',
      cardHolder: 'NNNNN NNNNNNN',
      expireMonth: 'MM',
      expireYear: 'YY',
      CCV: '000'
    }
    this.$emit('updateCard', blankCard)
  },
   props: {
        cards: Array
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
          if (this.cards.find((number) => number.cardNumber == this.newCard.cardNumber)){
            this.errorMessage ='Detta kort finns redan i din e-wallet!'
          } else if (this.newCard.vendor == '' ){
            this.errorMessage = 'Vänligen, välj en bank'
          } else if ( this.cards.find((cardVendor) => cardVendor.vendor == this.newCard.vendor)) {
            this.errorMessage = 'Du har redan ett kort av denna bank'
          } else if (this.newCard.expireYear == ''){
            this.errorMessage = 'Vänligen, fyll i giltighetsår'
          } else if (this.newCard.expireMonth == ''){
            this.errorMessage = 'Vänligen, fyll i giltighetsmånad'
          } else if (this.newCard.cardHolder == ''){
            this.errorMessage = 'Vänligen, fyll i kortinnehavarns namn'
          } else {
            this.errorMessage = ""
            this.$emit('send', {...this.newCard})
          }
        }
  }
}
</script>

<style scoped>

form p {
	margin: 0 0 0.2rem 0.5rem;
	align-self: flex-start;
	font-size: 0.8rem;
	font-weight: 600;
	color: rgba(0, 0, 0, 0.5);
	padding: 0;
}

input[type=text] {
  box-sizing: border-box;
  margin: 0 0 0.5rem 0;
  width: 100%;
  max-width: 21rem;
  border: 1px solid;
  border-radius: 0.5rem;
}

select {
  background-color: white;
  border-style: none;
  border: 1px solid;
  border-radius: 0.5rem;
}

form {
  margin: 2rem 1rem;
  min-height: 20rem;
  max-width: 21rem;
  min-width: 18rem;
  width: 80vw;
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  align-items: space-evenly;
}

form  * {
  padding: 1rem 1.5rem;
  font-size: 1rem;
  text-transform: uppercase;
  
}
  /* display: grid;
  grid-template-areas: 
    "number number number",
    "name name name",
    "expire-date . ccv",
    "vendor vendor vendor",
    ". button .";
}

.num {
  height: 2rem;
  grid-area: number;
}

.name {
  grid-area: name;
  height: 2rem;
}
 */

.valid-label {
	margin: 0.5rem 0 -0.2rem 3.2rem;
}

.expireDate-CCV {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  height: 5rem;
  padding: 0;
  margin: 0.5rem 0;
} 

.expireDate-CCV select {
  width: 30%;
  margin-right: 0.3rem;
}

.expireDate-CCV p {
  font-size: 0.65rem;
}

.expireDate-CCV p:nth-last-child(2){
  margin:0 0 0.2rem 1rem;
  }

 .ccv {
  width: 2.5rem;
  margin-left: auto;
  -webkit-appearance: none;
  -moz-appearance: textfield;
  border: 1px solid;
  border-radius: 0.5rem;
} 



.vendor {
  /* grid-area: vendor; */
  width: 100%;
  /* margin-top: 0.5rem; */
} 

.add-card-button {
  grid-area: button;
  padding: 1rem;
  margin: 1rem;
} 

.error {
	color: orangered;
}

</style>