<template lang="html">

  <section class="src-components-usuarios">
    <div class="jumbotron">
      <button class="btn btn-danger my-3 mr-3" @click="getUsuariosXML()">Pedir XMLHttpRequest</button>    
      <button class="btn btn-warning my-3 mr-3" @click="getUsuariosFetch()">Pedir FETCH</button>    
      <button class="btn btn-success my-3 mr-3" @click="getUsuariosAxios()">Pedir AXIOS</button>  
      <button class="btn btn-secondary my-3 mr-3" @click="limpiar()">Limpiar</button>  
      <h1>Usuarios</h1>
        <div class="table-responsive">
          <table class="table">
              <tr class="bg-success text-white">
                  <th>Nombre</th>
                  <th>E-mail</th>
                  <th>Telefono</th>
              </tr>
              <tr class="bg-info text-white" v-for="(usuario,index) in listaUsuarios" :key="index">
                  <td>{{ usuario.nombre }}</td>
                  <td>{{ usuario.email }}</td>
                  <td>{{ usuario.telefono }}</td>
              </tr>
          </table>
        </div>    
    </div>
  </section>
</template>

<script lang="js">

  export default  {
    name: 'src-components-usuarios',
    props: [],
    mounted () {

    },
    data () {
      return {
        listaUsuarios: [],
        url: 'https://609dbea233eed80017957098.mockapi.io/usuarios',
      }
    },
    methods: {
        getUsuariosXML() {
            let xhr = new XMLHttpRequest
            xhr.open('get',this.url)
            xhr.addEventListener('load', () => {
              if(xhr.status == 200) {
                this.listaUsuarios = JSON.parse(xhr.response)
              }
              else {
                console.error(`Error en GET -> status: ${xhr.status}`)
              }
            })
            xhr.addEventListener('error', e => {
                console.error(`Error XMLHttpRequest ->`, e)
            })
            xhr.send()
        },
        getUsuariosFetch() {
          fetch(this.url)
          .then(datos => datos.json())
          .then(respuesta => {
            this.listaUsuarios = respuesta
          })
          .catch(error => console.error(error))
        },
        getUsuariosAxios() {
          this.axios(this.url)
          .then( respuesta => {
            this.listaUsuarios = respuesta.data
          })
          .catch(error => console.error(error))
        },
        limpiar() {
          this.listaUsuarios = []
        }
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-usuarios {
  }
  .jumbotron {
      background-color: rgb(22, 22, 70);
      color: white;
  }
</style>
