<template>
    <div class="mt-4">
        <h1>
            {{ title }}
        </h1>
        <table class="table">
            <thead>
            <tr>
                <th scope="col">#</th>
                <th scope="col">Başlık</th>
                <th scope="col">Kategori</th>
                <th scope="col">Adet</th>
                <th scope="col">Fiyat</th>
                <th scope="col">İşlem</th>
            </tr>
            </thead>
            <tbody>
            <tr class="align-items-center" v-for="envanter in envanterler" :key="envanter.id">
                <th scope="row">{{ envanter.id }}</th>
                <td>{{ envanter.baslik}}</td>
                <td>{{ envanter.kategori }}</td>
                <td>{{ envanter.adet}}</td>
                <td>{{envanter.fiyat}} TL </td>
                <td>
                    <button class="btn btn-primary" @click.prevent="aktifpasif(envanter.id)">{{ button }}</button>
                    <button class="btn btn-danger ml-2" @click.prevent="sil(envanter.id)">Sil</button>
                </td>
            </tr>
            <tr>
                <td></td>
                <td></td>
                <td><b>Toplam: </b></td>
                <td>{{toplamadet}}</td>
                <td>{{toplamfiyat}}</td>
                <td></td>
            </tr>
            </tbody>
        </table>
    </div>
</template>
<script>
    export default  {
        props:{
            'active':{ type: Boolean },
            envanterler:{ default: []}
        },
        data(){
            return{
                title:{type:String},
                button:{type:String},
            }
        },
        created() {
            if(this.active==true){
                this.title="Aktif Kayıtlar";
                this.button="Arşivle";
            }
            else{
                this.title="Arşiv Kayıtları";
                this.button="Aktif et";
            }
        },
        methods:{
            aktifpasif(id){
                var index = this.$parent.$data.envanterler.map(x => {
                    return x.id;
                }).indexOf(id);
                this.$parent.$data.envanterler[index].aktif=!this.$parent.$data.envanterler[index].aktif;

            },
            sil(id){
                var index = this.$parent.$data.envanterler.map(x => {
                    return x.id;
                }).indexOf(id);
                this.$parent.$data.envanterler.splice(index,1);
            }
        },
        computed:{
            toplamadet(){
                var toplam=0;
                this.envanterler.forEach(e=>toplam+=e.adet);
                return toplam;
            },
            toplamfiyat(){
                var toplam=0;
                this.envanterler.forEach(e=>toplam+=e.fiyat);
                return toplam;
            }
        }


    }
</script>