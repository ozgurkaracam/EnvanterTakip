<template>
  <div>
    <Navbar @search="search"/>

    <div class="container">
      <h1 class="text-gray mt-4">Envanter Kayıt Formu</h1>
      <div class="row">
        <div class="col-md-12">
          <envanter-ekle />
        </div>

      </div>
      <hr>
      <div class="row">
        <div class="col-md-6">
          <Table :active="true" :envanterler="aktifkayitlar" />
        </div>
        <div class="col-md-6">
          <Table :active="false" :envanterler="pasifkayitlar" />
        </div>
      </div>


    </div>


  </div>
</template>

<script>
import Navbar from './components/Navbar'
import EnvanterEkle from './components/EnvanterEkle'
import Table from './components/Table'
export default {
  name: 'app',
  components: {
    Navbar,
    EnvanterEkle,
    Table
  },
  methods:{
    search(val){
      // this.envanterler.filter(e=>e.baslik==val);
      this.filteredItems=[];
      this.envanterler.forEach(e=>{
        if(e.baslik!='' && e.baslik.includes(val))
          this.filteredItems.push(e)
      });
    }
  },
  data(){
    return{
      filteredItems:[],
      envanterler:[
              {
                id:1,
        baslik:"Muz",
        kategori:"Meyve",
        adet:10,
        fiyat:20,
        aktif:true
              },
        {
          id:2,
          baslik:"Armut",
          kategori:"Meyve",
          adet:20,
          fiyat:15,
          aktif:true
        },
        {
          id:3,
          baslik:"Sigara",
          kategori:"Tütün",
          adet:5,
          fiyat:60,
          aktif:false
        }
      ]
    }
  },
  watch: {
      envanterler(){
        this.aktifkayitlar=this.envanterler.filter(e=>e.aktif==true);
        this.pasifkayitlar=this.envanterler.filter(e=>e.aktif==false);
      }
  },
  created() {
    this.filteredItems=this.envanterler;
  },
  computed: {
    aktifkayitlar: {
      get: function(){
        return this.filteredItems.filter(e=>e.aktif==true);
      },
      set: function(){

      }
    },
    pasifkayitlar:{
     get(){
       return this.filteredItems.filter(e=>e.aktif==false);
     },
      set(){

      }
    }
  }

}
</script>

<style>
</style>
