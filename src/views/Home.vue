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
    data: () => ({
        currentQuestion: {
            q: "Liker du jazz?",
            y: {
                next: "q2",
                text: "Ja"
            },
            n: {
                next: "q3",
                text: "Nei"
            }
        },
        questions: {
            q1: {
                q: "Liker du jazz?",
                y: {
                    next: "q2",
                    text: "Ja"
                },
                n: {
                    next: "q3",
                    text: "Nei"
                }
            }
        }
    }),
    methods: {
        clickYes() {
            alert("You pressed Yes!!!")
        },
        clickNo() {
            ""
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
