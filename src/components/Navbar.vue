<template>
    <nav class="navbar navbar-light bg-primary">
        <a class="navbar-brand text-white ml-5" href="#">
            Envanter takip sistemi
        </a>
        <form class="form-inline my-2 my-lg-0 mr-5" method="POST">
            <input class="form-control mr-sm-2" type="search" v-model="srch" placeholder="Search" aria-label="Search">
            <button class="btn btn-success my-2 my-sm-0" @click.prevent="$emit('search',srch)" type="submit">Search</button>
        </form>
    </nav>
</template>
<script>
    export default {
        data(){
            return{
                srch:null
            }
        },
        watch:{
            srch(){
                    this.$emit('search',this.srch);
            }
        }
    }
</script>