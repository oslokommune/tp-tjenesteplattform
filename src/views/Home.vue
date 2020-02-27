<template>
  <div class="home">
		<h1>Tjenesteplattformen</h1>
      <div class="WizardStep">
          <div>
              <div v-if="currentQuestion.lastStep">
                  <span class="tada">🎉</span>
                  <h2>{{ currentQuestion.message }}</h2>
                  <a :href="currentQuestion.link">{{ currentQuestion.button }}</a>
              </div>
              <div v-else class="Question">{{ currentQuestion.q }}</div>
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
            currentQuestion: {q: "", answers: [{text: ""}, {text: ""}], lastStep: false},
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
                        }],
                    lastStep: false
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
                        }],
                    lastStep: false
                },
                finnesDetFraFor: {
                    q: "Finnes det fra før?",
                    answers: [
                        {
                            next: "dekkesBehov",
                            text: "Ja"
                        },
                        {
                            next: "oversikt",
                            text: "Usikker"
                        },
                        {
                            next: "trengsNyttKjoreMiljo",
                            text: "Nei"
                        }],
                    lastStep: false
                },
                dekkesBehov: {
                    q: "Dekker eksisterende app/løsning behovet ditt?",
                    answers: [
                        {
                            next: "taKontakt",
                            text: "Ja"
                        },
                        {
                            next: "taKontaktProduktEier",
                            text: "Nei"
                        }
                    ]
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
                        }],
                    lastStep: false
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
                        }],
                    lastStep: false
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
                        }],
                    lastStep: false
                },
                taKontakt: {
                    message: "Ta kontakt for gjenbruk",
                    button: "Gå til Kontakt",
                    link: "",
                    answers: [],
                    lastStep: true
                },
                taKontaktProduktEier: {
                    message: "Du trenger å ta kontakt med produkteier",
                    button: "Kontakt produkteieren",
                    link: "",
                    answers: [],
                    lastStep: true
                },
                oversikt: {
                    message: "Du trenger en oversikt over kommunens løsninger",
                    button: "Gå til Oversikten",
                    link: "",
                    answers: [],
                    lastStep: true
                },
                platform: {
                    message: "Tjenesten du trenger er Plattform",
                    button: "Gå til Plattform",
                    link: "https://oslokommune.github.io/tp-plattform/#/",
                    answers: [],
                    lastStep: true
                },
                infrastruktur: {
                    message: "Tjenesten du trenger er Infrastruktur",
                    button: "Gå til Infrastruktur",
                    link: "https://oslokommune.github.io/tp-infrastruktur/#/",
                    answers: [],
                    lastStep: true
                },
                dataplatform: {
                    message: "Tjenesten du trenger er Dataplattform",
                    button: "Gå til Dataplattform",
                    link: "https://oslokommune.github.io/tp-dataplattform/#/",
                    answers: [],
                    lastStep: true
                },
                utviklerportal: {
                    message: "Tjenesten du trenger er Utviklerportalen",
                    button: "Gå til Utviklerportalen",
                    link: "https://oslokommune.github.io/tp-utviklerportalen/#/",
                    answers: [],
                    lastStep: true
                },
                vetIkke: {
                    message: "Vi vet ikke hvordan vi kan hjelpe deg...😞",
                    button: "Prøv igjen",
                    link: "",
                    answers: [],
                    lastStep: true
                }
            }
        }),
        methods: {
            click(index) {
                this.currentQuestion = this.questions[this.currentQuestion.answers[index].next];
            },
            openLink(link) {
                routeData = this.$router
                open(link, self)
            }
        }
    }
</script>

<style lang="scss" scoped>

.tada {
    font-size: 60pt;
    margin-top: 7em;
}
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

.service {
    background-color: #ff8274;
    border: none;
    color: white;
    padding: 10px 25px;
    width: 15em;
    margin-right: 1em;
    text-align: center;
    text-decoration: none;
    font-size: 16px;
    vertical-align: top;
    min-height: 5em;
    cursor: pointer;

    &:hover {
        color: black;
        background: #e0adff;
        border-color: #e0adff;
        text-decoration: none;
    }

}
.Answer {
    background-color: #2a2859;
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
        color: black;
        background: #6fe9ff;
        border-color: #6fe9ff;
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
