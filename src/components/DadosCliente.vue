<template>
<!-- Template de dados do cliente no repositório -->
    <div>
        <div class="row">
            <div class="col-md-4">
                <div class="card" style="width: 18rem;">
                    <img id="img" class="card-img-top" :src="user.avatar_url" alt="">
                    <ul class="list-group list-group-flush">
                        <!-- Tags com os dados quantidade de repositório, seguidores e seguindo -->
                        <li class="list-group-item">Repositórios - <span class="badge badge-success">{{user.public_repos}}</span></li>
                        <li class="list-group-item">Seguidores - <span class="badge badge-primary">{{user.followers}}</span></li>
                        <li class="list-group-item">Seguindo - <span class="badge badge-info">{{user.following}}</span></li>
                        <li class="list-group-item" v-if="user.length !==0">URL -<span>{{user.url}}</span></li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    //Transferencia da lista com os dados do cliente no repositório
    props:['user']
}


</script>

<style scoped>
    /* Formatando altura e largura do avatar(imagem) do cliente  */
    #img{
        width: 60px;
        height: 60px;
        margin-top: 5px;
        
    }

</style>