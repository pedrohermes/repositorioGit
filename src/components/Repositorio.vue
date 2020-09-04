<template>
    <!-- Template com os dados do repositório -->
    <div class="card card-body nb-1">
        <div class="row">
            <!-- O name dos repositórios do cliente -->
            <div class="col-md-6"><a :href="repositorio.html_url" target="_blank">{{repositorio.name}}</a></div>
            <div class="col-md-6">
                <!-- Tags com o total de visualizações,comentários e likes do repositórios -->
                <span class="badge badge-primary">Star: {{repositorio.stargazers_count}}</span>
                <span class="badge badge-secondary">Watch: {{repositorio.watchers_count}}</span>
                <span class="badge badge-success">Forks: {{repositorio.forks_count}}</span>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    //Transferência da lista com os dados do repositório
    props:['repositorio']
}
</script>

