<template>
<div class="container">
        <h1>Comentários</h1>
        <hr/>
        <div class="form-tudo form-group">
            <p>
                <input placeholder="Nome" type="text" name="author"
                class="form-control" v-model="nome"/>
            </p>
            <p>
                <textarea placeholder="Adicionar um comentário público..." name="message"
                class="form-control" v-model="message"></textarea>
            </p>
            <button style="float: right;" v-on:click="adicionarComentario" type="submit" class="btn btn-primary">Comentar</button>
        </div>
        <br><br>
        <div class="list-group">
            <p v-if="comentarios.length <= 0">Sem comentarios...</p>
            <div class="list-group-item" v-for="(comentario, index)
             in todosComentarios" v-bind:key="index">
            <span class="ComentarioAutor">
                Autor: <strong>{{ comentario.nome }}</strong>
            </span>
            <p>{{ comentario.message }}</p>
            <div>
                <a href="#" v-on:click.prevent="ExcluirComentario(index)" title="Excluir">Excluir</a>
            </div>
            </div>
        </div>
        <hr>
    </div> 
</template>

<script>
export default{
    data(){
            return{
                comentarios:[],
                nome:'',
                message:''
            }
        },
        methods:{
            adicionarComentario(){
                // console.log("Cheguei!");
                // console.log(this.nome);
                // console.log(this.message);

                if(this.message.trim() === ''){
                    alert('Escreva um comentario!');
                    return;
                }

                this.comentarios.push({
                    nome: this.nome,
                    message: this.message
                });

                this.nome = '';
                this.message = '';
            },
            ExcluirComentario(index){
                console.log("Exclui comentario:", index);

                this.comentarios.splice(index, 1);
            } 
        },
        computed:{
            todosComentarios(){
                return this.comentarios.map(comentario =>({
                    ...comentario,
                    nome: comentario.nome.trim() === '' ? 'Anônimo' : comentario.nome
                }))
            }
        },
        watch:{
            comentarios(val){
                console.log('valor',val)
            }
        }

}
</script>