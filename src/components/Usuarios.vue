<template>

  <section class="src-components-usuarios">
   <div class="jumbotron">
    <h1>Metodo POST</h1>
      <button class="btn btn-success my-3 mr-3" @click="getPostsFetch()">Fetch</button>
      <button class="btn btn-success my-3 mr-3" @click="getPostsAxios()">Axios</button>
      <button class="btn btn-warning my-3 mr-3" @click="borrar()">borrar</button>


      <!----------------------TABLA--------------------------------------------------------------->
      <div>
      <table class="table table-dark">
          <tr>
            <th>Nombre</th>
            <th>Email</th>
            <th>Edad</th>
          </tr>
          <tr v-for="usuario in usuarios" :key="usuario.email ">
            <td>{{usuario.nombre }}</td>
            <td>{{ usuario.email }}</td>
            <td>{{ usuario.edad }}</td>
          </tr>
        </table>
      </div>
   </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-components-usuarios',
    props: [],
    mounted () {
    
    },
    data () {
      return {
      ruta:"https://635723ad9243cf412f93b0b0.mockapi.io/usuarioss",
      usuarios:[]
      }
    },
    methods: {
      async getPostsAxios() {
        try {
          let post = await this.axios(this.ruta)
          this.usuarios = post.data
          if(this.usuarios.length == 0){
            alert("No hay usuarios disponibles")
          }
        }
        catch(error) { console.error(error) } 

      },
      borrar(){
        this.usuarios=[]
      },
      async getPostsFetch() {
        try {
          let response = await fetch(this.ruta)
          console.log(response)
          let respuesta = await response.json()
          this.usuarios = respuesta
          if(this.usuarios.length == 0){
            alert("No hay usuarios disponibles")
          }
        }
        catch(error) {
          console.error(error)
        }
      }

        },
    computed: {

    }
}


</script>

<style scoped lang="css">
.jumbotron {
  background-color: teal;
  color: white;
}

hr {
  background-color: #bbb;
}
</style>
