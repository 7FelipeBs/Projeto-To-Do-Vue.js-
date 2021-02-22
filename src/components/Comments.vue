<template>
      <div class="container">
            <h1>Comentários</h1>
            <hr/>
            <FormToDo v-on:add-todo="addComment"></FormToDo>
            <div class="list-group">
            <p v-if="comments.length <= 0">Sem comentarios...</p>
                <div class="list-group-item" v-for="(comment, index) in allComments" v-bind:key="index">
                    <span class="comment_author">Autor: <strong>{{ comment.name }}</strong></span>

                    <p>{{ comment.message }}</p>

                    <div>
                        <a href="#" title="Excluir"  v-on:click.prevent="removeComment(index)">Excluir</a>
                    </div>
                </div>
            </div>
            <hr>
        </div>  
</template>

<script>
import FormToDo from './FormToDo'
export default {
    components: {
        FormToDo
    },

    data(){
        return{
            comments: []
        }
    },

    methods: {
        addComment(comment){
            this.comments.push(comment)
        },
        removeComment(index){
            this.comments.splice(index, 1);
        }
    },

    computed: {
      allComments() {
        //Isso retorna um novo array, customizando a variavel Name
        return this.comments.map(comment => ({
          ...comment,
          name: comment.name.trim() === '' ? 'Anonimo' : comment.name
        }))
      }
    },

    watch: {
      comments(val){
        console.log('val', val)
      }
    }
    }
</script>