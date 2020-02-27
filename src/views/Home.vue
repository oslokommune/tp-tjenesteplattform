<template>
  <div class="home">
		<h1>Velkommen til tjenesteplattformen</h1>
      <div class="WizardStep">
          <div>
              <div class="Quesion">{{ currentQuestion.q }}</div>
              <button class="Yes" @click="clickYes()">{{ currentQuestion.y.text }}</button>
              <button class="No" @click="clickNo()">{{currentQuestion.n.text}}</button>
          </div>
      </div>
  </div>

</template>

<script>
// @ is an alias to /src

export default {
    name: 'Home',
    mounted: function() { this.currentQuestion = this.questions.q1 },
    data: () => ({
        currentQuestion: { q:"", y: {text:""}, n: {text:""}},
        questions: {
            q1: {
                q: "Liker du q1?",
                y: {
                    next: "q1",
                    text: "Ja"
                },
                n: {
                    next: "q2",
                    text: "Nei"
                }
            },
            q2: {
                q: "Liker du q2?",
                y: {
                    next: "q1",
                    text: "Ja"
                },
                n: {
                    next: "q3",
                    text: "Nei"
                }
            },
            q3: {
                q: "Liker du q3?",
                y: {
                    next: "q2",
                    text: "Ja"
                },
                n: {
                    next: "q4",
                    text: "Nei"
                }
            },
            q4: {
                q: "Hva liker du?",
                y: {
                    next: "q2",
                    text: "Rock"
                },
                n: {
                    next: "q1",
                    text: "Klassisk"
                }
            }
        }
    }),
    methods: {
        clickYes() {
            this.currentQuestion = this.questions[this.currentQuestion.y.next];
        },
        clickNo() {
            this.currentQuestion = this.questions[this.currentQuestion.n.next];
        }
    }
}
</script>

<style lang="scss" scoped>
p {
	font-family: 'Oslo Sans', Avenir, Helvetica, Arial, sans-serif;
}
p.old {
	font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
