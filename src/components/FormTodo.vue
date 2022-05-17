<template>
  <form class="d-block m-auto">
    <div class="form-group py-1">
      <label for="name" class="mb-1">Nome</label>
      <input v-model="name" type="text" class="form-control" id="name" aria-describedby="name" placeholder="Seu nome">
    </div>
    <div class="form-group py-1">
      <label for="comentario" class="mb-1">Comentário</label>
      <textarea v-model ="message" name="comentario" class="form-control" id="comentario" placeholder="Seu comentário.."></textarea>
    </div>
    <button v-on:click.prevent="addComment" type="submit" class="btn btn-primary my-2">Comentar</button>
  </form>
</template>

<script>
  export default {
    data() {
      return {
        name: '',
        message: ''
      }
    },
    methods: {
      addComment() {
        if (this.message.trim() === '') {
          return;
        }

        this.$emit('add-todo', {
          name: this.name,
          message: this.message,
        });

        this.name = '';
        this.message = '';
      }
    }
  }
  
</script>