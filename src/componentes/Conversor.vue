<template>
    <section class="src-componentes-Conversor">
       <div class="jumbotron">
           <h1>Conversor de Dolares</h1>
           <span>Ingrese monto $</span> <input type="text" v-model="monto">
           <br>
           <br>
           <span>Valor del dolar en $</span> <input type="text" v-model="valorDolar" ><span>- Actualizacion </span><input type="Checkbox" @click="ActualizarDolar()" v-model="valorDolar">
           <span v-if="checkOn" class="ml-3">{{new Date().toLocaleString()}}</span>
           <br>
           <br>
           <h3>Valor Convertido USD {{monto | Conversor(valorDolar)}}</h3>

           <h1 class="mt-5">Respuestas Choice</h1>
           <h5>1 : C</h5>
           <h5>2 : B</h5>
           <h5>3 : C</h5>
           <h5>4 : A</h5>
           <h5>5 : B y C</h5>
       </div>
  </section>
</template>

<script>
  export default  {
    name: 'src-componentes-Conversor',
    props: [],
    filters:{
        Conversor : function(value,valorDolar) {
            return value == 0? 0: (value/valorDolar)
      },
    },
    mounted () {
      this.pedirDatosAlServidor()

    },
    data () {
      return {
         ApiDolar : 'https://www.dolarsi.com/api/api.php?type=valoresprincipales',  
         monto: 0,
         valorDolar: 0,
         checkOn: false,
         intervalo: null
        }
    },
    methods: {
      async pedirDatosAlServidor() {
        try {
            let respuesta = await this.axios(this.ApiDolar)
            let datos = respuesta.data
            console.log('Datos GET', datos)
            this.valorDolar = Number(datos.find(dato => dato.casa.nombre == 'Dolar Blue').casa.venta.replace(',','.'))
            console.log(this.valorDolar)
        }
        catch(error) {
            console.error('Error en recepción de datos del servidor')
        }
        },
        ActualizarDolar(){
            this.checkOn = !this.checkOn
            console.log(this.checkOn)
            if(this.checkOn){
                this.intervalo = window.setInterval(this.pedirDatosAlServidor, 2000)
            }else{
                clearInterval( this.intervalo)
            }
        }
     
    },
    computed: {

    }
}
</script>

<style scoped lang="css">
  .src-componentes-Conversor {
      }
  
    
</style>