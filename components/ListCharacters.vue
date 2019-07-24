<template>
  <div class="row columns is-multiline cards-container">
    <div v-for="character in characters" :key="character.id" class="column is-one-quarter">
      <div class="card large">
        <div class="card-image">
          <figure class="image">
            <img :src="character.img" :title="character.name" :alt="character.name" />
          </figure>
        </div>
        <div class="card-content">
          <div class="media">
            <div class="media-content">
              <p class="title is-4 no-padding">Nome: {{character.name }}</p>
              <p class="subtitle is-6">Apelido: {{character.nickname }}</p>
            </div>
          </div>
          <div class="content">
            <ul>
              <li>
                Ocupação:
                <span
                  v-for="occupation in character.occupation"
                  :key="occupation"
                >{{ occupation }}</span>
              </li>
              <li>
                Aparições em temporadas:
                <span
                  v-for="appearance in character.appearance"
                  :key="appearance"
                >{{ appearance }}</span>
              </li>
              <li>Retratado por: {{character.portrayed }}</li>
              <li>Status: {{character.status }}</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    characters: {
      type: Array,
      required: true
    }
  }
};
</script>
