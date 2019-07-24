<template>
  <div class="row columns is-multiline cards-container is-clearfix">
    <div v-for="episode in episodes" :key="episode.id" class="column is-one-third">
      <div class="card large">
        <div class="card-content">
          <div class="media">
            <div class="media-content">
              <p class="title is-4 no-padding">{{ episode.title }}</p>
              <p class="subtitle is-4">Tempoarada: {{ episode.season }}</p>
            </div>
          </div>
          <div class="content">
            <b>Episódio:</b>
            {{episode.episode }}
            <br />
            <b>Data de Estreia:</b>
            {{episode.air_date }}
            <br />
            <b>Personagens:</b>
            <span v-for="actor in episode.characters" :key="actor">{{ actor }},</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    episodes: {
      type: Array,
      required: true
    }
  }
};
</script>
