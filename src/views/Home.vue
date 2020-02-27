<template>
  <div class="home">
		<h1>Velkommen til tjenesteplattformen</h1>
      <div class="WizardStep">
          <div>
              <div class="Question">{{ currentQuestion.q }}</div>
              <div class="container">
                  <div v-for="(answer, index) in currentQuestion.answers">
                    <button class="Answer" @click="click(index)">{{ answer.text }}</button>
                  </div>
              </div>

          </div>
      </div>
  </div>

</template>

<script>
    // @ is an alias to /src

    export default {
        name: 'Home',
        mounted: function () {
            this.currentQuestion = this.questions.innledning
        },
        data: () => ({
            currentQuestion: {q: "", answers: [{text: ""}, {text: ""}]},
            questions: {
                innledning: {
                    q: "Skal du lage eller dele noe?",
                    answers: [
                        {
                            next: "nyEllerEksisterende",
                            text: "Jeg har en ny eller eksisterende løsning som jeg skal lage noe på"
                        },
                        {
                            next: "dataEllerApi",
                            text: "Jeg har noe jeg ønsker å dele"
                        }]
                },
                nyEllerEksisterende: {
                    q: "Skal du lage en ny app/løsning eller har du en eksisterende app/løsning?",
                    answers: [
                        {
                            next: "finnesDetFraFor",
                            text: "Jeg skal lage en ny app/løsning"
                        },
                        {
                            next: "trengsNyttKjoreMiljo",
                            text: "Jeg har en eksisterende app/løsning"
                        }]
                },
                finnesDetFraFor: {
                    q: "Finnes det fra før?",
                    answers: [
                        {
                            next: "taKontakt",
                            text: "Ja"
                        },
                        {
                            next: "oversikt",
                            text: "Usikker"
                        },
                        {
                            next: "trengsNyttKjoreMiljo",
                            text: "Nei"
                        }]
                },
                trengsNyttKjoreMiljo: {
                    q: "Trenger du et nytt kjøremiljø?",
                    answers: [
                        {
                            next: "platform",
                            text: "Ja"
                        },
                        {
                            next: "trengerDuOvervakning",
                            text: "Nei"
                        }]
                },
                trengerDuOvervakning: {
                    q: "Trenger du overvakning?",
                    answers: [
                        {
                            next: "infrastruktur",
                            text: "Ja"
                        },
                        {
                            next: "vetIkke",
                            text: "Nei"
                        }]
                },
                dataEllerApi: {
                    q: "Trenger du data eller API?",
                    answers: [
                        {
                            next: "dataplatform",
                            text: "Jeg har data eller trenger data"
                        },
                        {
                            next: "utviklerportal",
                            text: "Jeg har API eller trenger API"
                        }]
                },
                taKontakt: {
                    q: "TA KONTAKT FOR GJENBRUK!!!",
                    answers: []
                },
                oversikt: {
                    q: "HER ER EN OVERSIKT!!!",
                    answers: []
                },
                platform: {
                    q: "PLATTFORM!!!",
                    answers: []
                },
                infrastruktur: {
                    q: "INFRASTRUKTUR!!!",
                    answers: []
                },
                dataplatform: {
                    q: "DATAPLATTFORM!!!",
                    answers: []
                },
                utviklerportal: {
                    q: "UTVIKLERPORTALEN!!!",
                    answers: []
                },
                vetIkke: {
                    q: "VI VET IKKE!!!",
                    answers: []
                }
            }
        }),
        methods: {
            click(index) {
                this.currentQuestion = this.questions[this.currentQuestion.answers[index].next];
            }
        }
    }
</script>

<style lang="scss" scoped>

h1 {
    margin-top: 2em;
}
.container {
    display: flex;
    align-items: flex-start;
    justify-content: center;
}

.Question {
    margin-bottom: 2em;
}

.Answer {
    background-color: #ff8274; /* Green */
    border: none;
    color: white;
    padding: 15px 32px;
    width: 15em;
    margin-right: 1em;
    text-align: center;
    text-decoration: none;
    font-size: 16px;
    vertical-align: top;
    min-height: 10em;
    cursor: pointer;

    &:hover {
        color: white;
        background: hotpink;
        border-color: hotpink;
        text-decoration: none;
    }

}
p {
	font-family: 'Oslo Sans', Avenir, Helvetica, Arial, sans-serif;
}
p.old {
	font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
