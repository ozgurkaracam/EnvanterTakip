<template>
    <div class="col-md-6">
        <form method="post" class="form">

            <label for="baslik" class="">Başlık</label>
            <input type="text" v-model="baslik" class="form-control" name="baslik" id="baslik">
            <label for="kategori"  class="">Kategori</label>
            <input type="text" v-model="kategori" class="form-control" name="kategori" id="kategori">
            <label for="adet"  class="">Adet</label>
            <input type="number" v-model="adet" class="form-control" name="adet" id="adet">
            <label for="fiyat" class="">Fiyat</label>
            <input type="number" v-model="fiyat" class="form-control" name="fiyat" id="fiyat">
            <select v-model="aktif" class="form-control mt-3">
                <option :value="true" selected="selected">Aktif</option>
                <option :value="false">Arşiv</option>
            </select>
            <button type="submit" class="btn btn-primary mt-3" @click.prevent="envanterEkle">Kaydet</button>

        </form>
    </div>
</template>
<script>
    export default {
        methods:{
            envanterEkle(){
                this.$parent.$data.envanterler.push({
                    id:this.$parent.$data.envanterler.slice(-1)[0].id+1,
                    baslik:this.baslik,
                    kategori:this.kategori,
                    adet:parseInt(this.adet),
                    fiyat:parseInt(this.fiyat),
                    aktif:this.aktif
                });
                this.baslik=null;
                this.kategori=null;
                this.adet=null;
                this.fiyat=null;
                this.aktif=true;

            }
        },
        data(){
            return{
                baslik:null,
                kategori: null,
                adet: null,
                fiyat: null,
                aktif: true
            }
        }
    }
</script>