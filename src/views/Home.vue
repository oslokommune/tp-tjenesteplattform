<template>
  <div class="home">
      <div class="back-button-container" v-if="currentQuestion.backButtonEnabled">
          <button class="back-button" @click="goBack()">Gå tilbake</button>
      </div>
      <div class="WizardStep">
          <h1>Tjenesteguiden</h1>
          <div>
              <div v-if="currentQuestion.lastStep">
		            <img alt="success" src="https://media.giphy.com/media/xSM46ernAUN3y/giphy.gif"/>
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
            currentQuestion: {q: "", answers: [{text: ""}, {text: ""}], lastStep: false, backButtonEnabled: false},
            prevStates: [],
            questions: {
                innledning: {
                    q: "La oss hjelpe deg å finne rett tjeneste, skal du lage eller dele noe?",
                    answers: [
                        {
                            next: "nyEllerEksisterende",
                            text: "Jeg har en ny eller eksisterende løsning som jeg skal lage noe på"
                        },
                        {
                            next: "dataEllerApi",
                            text: "Jeg har noe jeg ønsker å dele"
                        }],
                    lastStep: false,
                    backButtonEnabled: false
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
                    lastStep: false,
                    backButtonEnabled: true
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
                    lastStep: false,
                    backButtonEnabled: true
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
                    ],
                  lastStep: false,
                  backButtonEnabled: true
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
                    lastStep: false,
                    backButtonEnabled: true
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
                    lastStep: false,
                    backButtonEnabled: true
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
                    lastStep: false,
                    backButtonEnabled: true
                },
                taKontakt: {
                    message: "Ta kontakt for gjenbruk",
                    button: "Gå til Kontakt",
                    link: "",
                    answers: [],
                    lastStep: true,
                    backButtonEnabled: true
                },
                taKontaktProduktEier: {
                    message: "Du trenger å ta kontakt med produkteier",
                    button: "Kontakt produkteieren",
                    link: "",
                    answers: [],
                    lastStep: true,
                    backButtonEnabled: true
                },
                oversikt: {
                    message: "Du trenger en oversikt over kommunens løsninger",
                    button: "Gå til Oversikten",
                    link: "",
                    answers: [],
                    lastStep: true,
                    backButtonEnabled: true
                },
                platform: {
                    message: "Tjenesten du trenger er Plattform",
                    button: "Gå til Plattform",
                    link: "https://oslokommune.github.io/tp-plattform/#/",
                    answers: [],
                    lastStep: true,
                    backButtonEnabled: true
                },
                infrastruktur: {
                    message: "Tjenesten du trenger er Infrastruktur",
                    button: "Gå til Infrastruktur",
                    link: "https://oslokommune.github.io/tp-infrastruktur/#/",
                    answers: [],
                    lastStep: true,
                    backButtonEnabled: true
                },
                dataplatform: {
                    message: "Tjenesten du trenger er Dataplattform",
                    button: "Gå til Dataplattform",
                    link: "https://oslokommune.github.io/tp-dataplattform/#/",
                    answers: [],
                    lastStep: true,
                    backButtonEnabled: true
                },
                utviklerportal: {
                    message: "Tjenesten du trenger er Utviklerportalen",
                    button: "Gå til Utviklerportalen",
                    link: "https://oslokommune.github.io/tp-utviklerportalen/#/",
                    answers: [],
                    lastStep: true,
                    backButtonEnabled: true
                },
                vetIkke: {
                    message: "Vi vet ikke hvordan vi kan hjelpe deg...😞",
                    button: "Prøv igjen",
                    link: "",
                    answers: [],
                    lastStep: true,
                    backButtonEnabled: true
                }
            }
        }),
        methods: {
            click(index) {
                this.prevStates.push(this.currentQuestion)
                this.currentQuestion = this.questions[this.currentQuestion.answers[index].next];
            },
            goBack() {
                this.currentQuestion = this.prevStates.pop()
            }
        }
    }
</script>

<style lang="scss" scoped>

.back-button {
    background-color: #2a2859;
    border: none;
    color: white;
    text-align: center;
    text-decoration: none;
    font-size: 16px;
    vertical-align: top;
    cursor: pointer;
    margin-top: 3em;
    padding: 1em;


    &:hover {
        color: black;
        background: #6fe9ff;
        border-color: #6fe9ff;
        text-decoration: none;
    }
}

.back-button-container {
    position: absolute;
}
h1 {
    margin-top: 2em;
    display: inline-block;
    font-size: 20px;
    margin-bottom: 1em;
}
.container {
    display: flex;
    align-items: flex-start;
    justify-content: center;
}

.Question {
    margin-bottom: 2em;
    font-size: 30px;
}

.WizardStep {
    text-align: center;
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

    :last-child {
        margin-right: 0;
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
