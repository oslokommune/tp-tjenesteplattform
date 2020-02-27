<template>
  <div class="home">
		<h1>Værsego'! Lag magi</h1>
      <div class="WizardStep">
          <div v-if="showQuestion1">
              <div class="Quesion">Liker du jazz?</div>
              <button class="Yes" @click="toggleQuestion1()">Ja</button>
              <button class="No" @click="showQuestion1 = false">Nei</button>
          </div>
      </div>
  </div>

</template>

<script>
// @ is an alias to /src

export default {
    name: 'Home',
    data: () => ({
        showQuestion1: true,
    }),
    methods: {
        toggleQuestion1() {
            this.showQuestion1 =
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
