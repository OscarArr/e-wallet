<template>
  <section>
      <h1>E-Wallet</h1>
      <button v-if="this.cards.length > 0" class="remove-card-btn" @click="showModal=true"><h6>REMOVE THIS CARD</h6></button>
      <h6>Active Card</h6>
      <div class="modal-background" v-if="showModal" @click.self="showModal=false">
          <div class="modal">
              <button class="close-btn" @click="showModal=false">x</button>
              <h4>Are you sure you want to remove this {{activeCard.vendor}} card?</h4>
                <div>
				<button class="remove-card" @click="removeCard">Yes</button>
				<button @click="showModal=false">No</button>  
              </div>
          </div>
      </div>
      <CardInfo v-if="activeCard" class="active-card" :renderCard="activeCard"/>
      <h6>Your Cards</h6>
      <div class="card-stack">
          <CardInfo v-for="card in cardsInStack" :key="card.cardNumber"
           @sendActiveCard="setActiveCard" :renderCard="card"/>
      </div>
      <button class="add-card-btn" @click="addCard">ADD NEW CARD</button>
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
        },
		removeCard(){
			this.cards.splice(0, 1)
			this.$emit('removedCard', this.cards)
			this.showModal = false
			this.activeCard = this.cards[0]
		}
    },
    data(){return{
        activeCard: null,
		showModal: false
    }}
}
</script>

<style lang="scss" scoped>

	.modal-background {
		position: fixed;
		top: 0;
		left: 0;
		height: 200%;
		width: 100vw;
		background-color: rgba(0, 0, 0, 0.84);

			.modal{
				background-color: white;
				border-radius: 1rem;
				width: 50%;
				min-width: 13rem;
				max-width: 18rem;
				margin: 5rem auto;
				padding: 2rem;
				display: flex;
				flex-direction: column;
				flex-wrap: wrap;

					.close-btn {
						width: 1.5rem;
						height: 1.5rem;
						align-self: flex-end;
						margin: -1rem -1rem 1.5rem 0;
						font-weight: 900;
						padding: 0;
						background-color: rgba(0, 0, 0, 0.04);
						border-radius: 0.2rem;
						border: 1px solid black;

							&:hover {
								box-shadow: 1px 1px 1px 1px rgba(0, 0, 0, 0.2);
								background-color: rgba(0, 0, 0, 0.03);
								border: 3px solid black;
							}
					}

					div {
						margin-top: 2rem;
						display: flex;
						justify-content: space-evenly;

						button {
							background-color: white;
							border: 2px solid black;
							border-radius: 0.3rem;
							width: 3rem;
							height: 2rem;
							padding: 0.3rem;
							box-shadow: 1px 1px 1px 1px rgba(0, 0, 0, 0.2);

							&:hover {
								background-color: rgba(0, 0, 0, 0.03);
								border: 3px solid black;
								box-shadow: 2px 2px 3px 1px rgba(0, 0, 0, 0.2);
							}
						}
					}
			}	
	}

	section {
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
		min-width: 20rem;
		max-width: 24rem;
	}

	.remove-card-btn {
		margin: 0 1rem -0.8rem auto;
		padding: 0.1rem;
		width: 7rem;
		border: 2px solid red;
		border-radius: 0.5rem;
		background-color: white;
		
			h6 {
				margin: 0;
				color: red;
			}

			&:hover {
				background-color: rgba(255, 0, 0, 0.15);
			}
	}

	h1 {
		margin-top: 0.5rem;
		flex-basis: 70%;
	}

	h6 {
		font-size: 0.7rem;
		flex-basis: 80%;
		margin: 1rem 0 0.2rem 0;

			&:nth-child(3) {
				margin: 0 0 0.2rem 0;
			}
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

	.add-card-btn {
		margin: 1rem 0;
		padding: 1rem;
		width: 90%;
		align-self: flex-end;
		background-color: white;
		border-radius: 0.5rem;
		border-style: none;
		border: 2px solid black;

			&:hover {
				box-shadow: 2px 2px 5px 3px rgba(0, 0, 0, 0.2), inset 8px 6px 8px 3px rgb(255, 255, 255), inset -4px -4px 2px 0 rgb(255, 255, 255);
				background-color: rgba(0, 0, 0, 0.05);
			}
	}

</style>