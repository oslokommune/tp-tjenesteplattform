<template>
  <div class="home">
		<h1>Velkommen til tjenesteplattformen</h1>
      <div class="WizardStep">
          <div>
              <div class="Quesion">{{ currentQuestion.q }}</div>

              <div v-for="(answer, index) in currentQuestion.answers">
                <button class="Answer" @click="click(index)">{{ answer.text }}</button>
              </div>
          </div>
      </div>
  </div>

</template>

<script>
// @ is an alias to /src

export default {
    name: 'Home',
    mounted: function() { this.currentQuestion = this.questions.innledning },
    data: () => ({
        currentQuestion: { q:"", answers: [{text:""}, {text:""}]},
        questions: {
            innledning: {
                q: "Skal du lage eller dele noe?",
                answers: [{
                    next: "q2",
                    text: "Jeg har en ny eller eksisterende løsning som jeg skal lage noe på"
                },
                {
                    next: "q3",
                    text: "Jeg har noe jeg ønsker å dele"
                },
                {
                    next: "q4",
                    text: "Visst faen"
                }]
            },
            q2: {
                q: "Liker du q2?",
                answers: [{
                    next: "innledning",
                    text: "Ja"
                },
                {
                    next: "q3",
                    text: "Nei"
                }]
            },
            q3: {
                q: "Liker du q3?",
                answers: [{
                    next: "q2",
                    text: "Ja"
                },
                {
                    next: "q4",
                    text: "Nei"
                }]
            },
            q4: {
                q: "Hva liker du?",
                answers: [{
                    next: "q2",
                    text: "Rock"
                },
                {
                    next: "innledning",
                    text: "Klassisk"
                }]
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
p {
	font-family: 'Oslo Sans', Avenir, Helvetica, Arial, sans-serif;
}
p.old {
	font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
