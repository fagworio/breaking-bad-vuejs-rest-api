<template>
  <section class="hero is-primary">
    <div class="hero-body">
      <div class="container">
        <div class="card">
          <div class="card-content">
            <div class="content">
              <div class="control has-icons-left has-icons-right">
                <input
                  type="search"
                  v-model="content"
                  @input="handleInput"
                  class="input is-large"
                  placeholder="Pesquisar"
                />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  prop: ["value"],
  data() {
    return {
      content: this.value
    };
  },
  methods: {
    handleInput(e) {
      this.$emit("input", this.content);
    }
  }
};
</script>


