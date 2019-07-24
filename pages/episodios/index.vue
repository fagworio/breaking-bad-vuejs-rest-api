<template>
<div>
 <SearchFilter v-model="search" />
<div class="section">
  <h1 class="title is-2 has-text-centered">Episódios</h1>
  <ListEpisodes :episodes="filteredEpisodes" />
  </div>
</div>
</template>

<script>
import ListEpisodes from "@/components/ListEpisodes";
import SearchFilter from "@/components/SearchFilter";
export default {
  components: {
    ListEpisodes,
    SearchFilter
  },
  data() {
    return {
      episodes: [],
      search: '',
      URL: 'https://www.breakingbadapi.com/api/episodes'
    };
  },
  created() {
    fetch(this.URL)
      .then(res => res.json())
      .then(res => (this.episodes = res))
      .catch(error => console.log(error));
  },
  computed: {
    filteredEpisodes() {
      return this.episodes.filter(episode => {
        return episode.title.toLowerCase().match(this.search.toLowerCase());
      });
    }
  }
}
</script>

