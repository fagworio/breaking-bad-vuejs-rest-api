<template>
  <div>
    <section class="hero is-medium is-primary is-bold">
      <div class="hero-body">
        <div class="container">
          <h1 class="title is-center">Envie sua sugestão</h1>
        </div>
      </div>
    </section>
    <div class="columns is-centered message">
      <div class="column is-half">
        <form @submit.prevent="onSubmitted" action="#" method="post">
          <div class="field">
            <h1 class="title">{{ message }}</h1>
            <div v-if="errors.length">
              <b>Por favor, corrija o(s) seguinte(s) erro(s):</b>
            </div>

            <div class="control">
              <input
                type="text"
                v-model="name"
                class="input is-primary is-medium"
                placeholder="Seu nome"
              />
            </div>
            <br />
            <div class="control">
              <textarea v-model="author" class="textarea is-primary" placeholder="authorm"></textarea>
            </div>
          </div>
          <input type="submit" class="button is-primary is-medium" value="Enviar Sugestão" />
        </form>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";

export default {
  data() {
    return {
      name: null,
      author: null,
      message: null,
      errors: [],
      URL:'https://frontendtestesamba.free.beeceptor.com/breaking-bad/suggestions'
    };
  },
  methods: {
    onSubmitted() {
      axios
        .post(this.URL, [this.name, this.author])
        .then(res => {
          this.message = res.data;
        })
        .catch(err => {
          this.errors.push(err);
        });
    }
  }
};
</script>

<style scoped>
.title {
  text-align: center;
}
.message {
  padding: 10px 10px;
}
.hero.is-medium .hero-body {
  padding-bottom: 7rem;
  padding-top: 7rem;
}
</style>

</style>
