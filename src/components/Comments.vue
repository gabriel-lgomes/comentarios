<template>
  <section>
        <div class="container"> 
          <h3 class="mt-3">Formulário de comentários</h3>
          <hr />
          <FormTodo v-on:add-todo="addComment"> </FormTodo>
          <h2 class="mt-3">Comentários</h2>
          <hr>
          <div class="list-group">
            <p v-if="comments.length === 0">Sem comentários...</p>
            <div class="list-group-item" v-for="(comment, index) in allComments" v-bind:key="index">
              <span class="comment__author">Autor: <strong>{{ comment.name }}</strong></span>
              <p>{{comment.message}}</p>
              <div>
                <a v-on:click.prevent="removeComment(index)" href="#" title="Excluir">Excluir</a>
              </div>
            </div>
          </div>
          <hr />
        </div>
      </section> 
</template>

<script> 

import FormTodo from './FormTodo';

export default {
  components: {
    FormTodo
  },
  data() {
    return {
      comments: []
    }
  },
  methods: {
    addComment(comment) {
      this.comments.push(comment);
    },
    removeComment(index) {
      this.comments.splice(index, 1);
    }
  },
  computed: {
    allComments() {
      return this.comments.map(comment => ({
        ...comment,
        name: comment.name.trim() === '' ? 'Anônimo' : comment.name
      }))
    }
  },
  watch: {
    comments() {
      this.comments.forEach(item => {
        localStorage.setItem(item.name, item.message);
      });
    }
  }
}
</script>
