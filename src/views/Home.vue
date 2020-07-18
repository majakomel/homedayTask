<template>
  <main>
    <form @submit.prevent="onSubmit" class="form">
      <label for="username" class="form__label">
        Type in the GitHub username you want to search for:
      </label>
      <div class="form__inputWrapper">
        <input
          type="text"
          id="username"
          class="form__input"
          name="username"
          autocomplete="off"
          placeholder="username"
          v-model="username"
          v-bind:class="{ 'form__input--errored': error }"
        />
        <div v-if="error" class="form__errorMsg">{{ error }}</div>
      </div>

      <button type="submit">Search</button>
    </form>
  </main>
</template>

<script>
export default {
  data: function() {
    return {
      username: "",
      error: null
    };
  },
  methods: {
    onSubmit() {
      this.error = null;
      if (!this.username) {
        this.error = "You have to type in the username.";
        return;
      }

      this.$router.push({
        name: "results",
        params: { username: this.username }
      });
    }
  }
};
</script>

<style lang="scss">
.form {
  &__inputWrapper {
    position: relative;
    margin-bottom: 20px;
  }
  &__input {
    width: 200px;
    &--errored {
      border: 1px solid red;
      border-radius: 4px;
    }
  }
  &__label {
    display: block;
    margin-bottom: 10px;
  }
  &__errorMsg {
    position: absolute;
    font-size: 12px;
    color: red;
  }
}
</style>
