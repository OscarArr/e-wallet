<template>
  <section>
      <h1>E-Wallet</h1>
      <h6>Active Card</h6>
      <CardInfo v-if="activeCard" class="active-card" :renderCard="activeCard"/>
      <h6>Your Cards</h6>
      <div class="card-stack">
          <CardInfo v-for="card in cardsInStack" :key="card.cardNumber"
           @sendActiveCard="setActiveCard" :renderCard="card"/>
      </div>
      <button @click="addCard">ADD NEW CARD</button>
  </section>
</template>

<script>
import CardInfo from "../components/CardInfo.vue"
export default {
	mounted(){
		this.activeCard = this.cards[0]
	},
    components: {CardInfo},
    props: {
        cards: Array
    },
    computed: {
        cardsInStack(){
            return this.cards.filter(card => card != this.activeCard)
        }
    },
    methods: {
        addCard(){
            this.$emit('changeView')
        },
        setActiveCard(newActiveCard){
            this.activeCard = newActiveCard
        }
    },
    data(){return{
        activeCard: null
    }}
}
</script>

<style lang="scss" scoped>

	section {
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
	}

	h1 {
		margin-top: 0.5rem;
		/* font-size: 1.3rem; */
	}

	h6 {
		font-size: 0.7rem;
		flex-basis: 100%;
		margin: 1rem 0 0.2rem 0;
	}

    /* .active-card {
		margin: 0.2rem 0 0.5rem 0;
	} */

    .card-stack{
        display: grid;
        grid-auto-rows: 15%;
        height: 22rem;
        /* margin-bottom: 1rem; */
		/* max-width: 21rem; */
		/* width: 90vw; */
		box-shadow: 0;
    }

	button {
		margin-bottom: 1rem;
		padding: 1rem;
		width: 90%;
		align-self: flex-end;
		background-color: white;
		border-radius: 0.5rem;
		border-style: none;
	}

</style>