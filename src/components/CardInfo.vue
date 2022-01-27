<template>
	<section v-if="renderCard" @click="$emit('sendActiveCard', renderCard)" :class="['card', classGenerator]">
		<div class="wifichip">
			<div class="wifi"></div>
			<div class="chip"></div>
		</div>
		<div class="logo"></div>
		<p v-if="renderCard" class="card-number">{{cardNumber}}</p>
		<div class="cardholder-name">
			<p>CARDHOLDER NAME</p>
			<p class="cardholder">{{name}}</p>
		</div>
		<div class="valid-date">
			<p>VALID THRU</p>
			<p>{{expireMonth}}/{{expireYear}}</p>
		</div>
	</section>
</template>

<script>
export default {
	updated(){
		// console.log(this.card)
		// this.dataLoaded = true
		// console.log(this.dataLoaded)
	},
	props:{
		renderCard: Object
	},
	data(){return{
		// dataLoaded: false
	}},
	computed:{
		cardNumber(){
			if(this.renderCard.cardNumber){
				let fakeNumber = "################"
				let printNumber = this.renderCard.cardNumber + fakeNumber.substring(0, (16-this.renderCard.cardNumber.length))
				
				return (printNumber.substring(0, 4) + " " +
				printNumber.substring(4, 8) + " " + 
				printNumber.substring(8, 12) + " " +
				printNumber.substring(12, 16) + " ")
			} else {
				return "#### #### #### ####"
			}
		},
		name(){
			return this.renderCard.cardHolder ? this.renderCard.cardHolder : "NNNNN NNNNNNNN"
		},
		expireMonth(){
			return this.renderCard.expireMonth ? this.renderCard.expireMonth : "MM"
		},
		expireYear(){
			return this.renderCard.expireYear ? this.renderCard.expireYear : "YY"
		},
		classGenerator(){
			return this.renderCard.vendor ? this.renderCard.vendor : "empty"
		}
	}
}
</script>

<style scoped>
.card * {
	text-shadow: -1px 1px 0px rgba(0, 0, 0, 0.3), 0px -0.5px 1px rgba(0, 0, 0, 0.3)
}

.card {
	max-width: 21rem;
	min-width: 19rem;
	width: 80vw;
	/* margin: 1rem 1rem; */
	max-height: 13rem; 
	min-height: 11.74rem; 
	height: calc(80vw * 0.618);
	background-color: darkgray;
	border-radius: 0.5rem;
	box-shadow: 3px 3px 5px 0px rgba(0,0,0,0.5);
	padding: 1.5rem 1rem;

	display: grid;
	grid-template-areas: 
	"wifichip logo"
	"cardNumber cardNumber"
	"cardHolder validDate";
}

.card-number {
	grid-area: cardNumber;
	font-size: 1.6rem;
}

.cardholder-name {
	grid-area: cardHolder;
	font-size: 1rem;
	align-self: flex-end;
	text-align: start;
	text-transform: uppercase;
}

.cardholder-name p:first-child {
	font-size: 0.7rem;
}

.valid-date {
	grid-area: validDate;
	font-size: 0.7rem;
	align-self: flex-end;
	text-align: end;
}

.valid-date p:nth-child(2){
	font-size: 1rem;
}

.wifichip {
	grid-area: wifichip;
}

.logo{
	grid-area: logo;
	justify-self: flex-end;
	height: 3rem;
	width: 3rem;
	background-size: contain;
	background-repeat: no-repeat;
}

.chip {
	/* background-image: url("../assets/chip.svg"); */
	background: url("../assets/chip.svg"), linear-gradient(90deg, rgba(179,176,174,1) 0%, rgba(223,207,189,1) 65%);
	border-radius: 8px;
}
.chip, .wifi {
	height: 2.4rem;
	width: 3rem;
	background-size: contain;
	background-repeat: no-repeat;
}

.valid-MY {
	display: flex;
	justify-content: center;
	align-items: center;
}


/* vendor card styles */

.empty .wifichip .wifi {
	background-image: url("../assets/wifi.svg");
	background-repeat: no-repeat;
}

.bitcoin {
	background: linear-gradient(248.04deg, rgba(255, 255, 255, 0.15) 0%, rgba(255, 255, 255, 0) 99.07%), #FFAE34;
}

.bitcoin .wifichip .wifi {
	background-image: url("../assets/wifi.svg");
	background-repeat: no-repeat;
}
.bitcoin .logo {
	background-image: url("../assets/bitcoin.svg");
	background-repeat: no-repeat;
}

.blockchain {
	background: linear-gradient(248.52deg, rgba(0, 0, 0, 0.15) 1.49%, rgba(0, 0, 0, 0) 100%), #8B58F9;
	color: white;
	text-shadow: -1px 1px 0px rgba(255, 255, 255, 0.3), 0px -0.5px 1px rgba(255, 255, 255, 0.3)
}

.blockchain .logo {
	background-image: url("../assets/blockchain.svg");
}

.blockchain .wifichip .wifi {
	background-image: url("../assets/wifi_white.svg");
	background-repeat: no-repeat;
}

.evil {
	background: linear-gradient(248.3deg, rgba(0, 0, 0, 0.16) 0%, rgba(0, 0, 0, 0) 100%), #F33355;
	color: white;
	text-shadow: -1px 1px 2px rgba(255, 255, 255, 0.3), 0px -0.5px 1px rgba(255, 255, 255, 0.3)
}

.evil .logo {
	background-image: url("../assets/evil.svg");
}

.evil .wifichip .wifi {
	background-image: url("../assets/wifi_white.svg");
	background-repeat: no-repeat;
}

.ninja {
	background: linear-gradient(248.3deg, rgba(255, 255, 255, 0.15) 0%, rgba(255, 255, 255, 0) 100%), #222222;
	color: white;
	text-shadow: -1px 1px 0px rgba(255, 255, 255, 0.3), 0px -0.5px 1px rgba(255, 255, 255, 0.3)
}

.ninja .logo {
	background-image: url("../assets/ninja.svg");
}

.ninja .wifichip .wifi {
	background-image: url("../assets/wifi_white.svg");
	background-repeat: no-repeat;
}

</style>