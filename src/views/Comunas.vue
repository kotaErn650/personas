<template>
  <div class="container">
    <h1>Listado de comunas |
      <button @click="text-start"
        class="btn btn-success mx-2">
        <font-awesome-icon icon="plus" />
      </button>
    </h1>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Code</th>
          <th scope="col">Name</th>
          <th scope="col">Municipality</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(comuna, index) in comunas" :key="index">
          <th scope="row">{{ index + 1 }}</th>
          <td>{{ comuna.comu_codi }}</td>
          <td>{{ comuna.comu_nomb }}</td>
          <td>{{ comuna.muni_nomb }}</td>
          <td>
            <button
              @click="deleteComuna(comuna.comu_codi)"
              class="btn btn-warning mx-2"
            >
              <font-awesome-icon icon="trash" />
            </button>
            <buttton
              @click="editComuna(comuna.comu_codi)"
              class="btn btn-warning mx-2"
            >
              <font-awesome-icon icon="pencil" />
            </buttton>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>


import axios from "axios";
import Swal from "sweetalert2";

export default {
  name: "ComunaV",
  data() {
    return {
      comunas: [],
    };
  },
  /**
   *
   */
  methods: {
    deleteComuna(codigo) {
      Swal.fire({
        title: `Do you want tio delete the Comuna with is ${codigo}`,
        showCancelButton: true,
        confirmButtonText: "Delete",
      }).then((result) => {
        if (result.isConfirmed) {
          axios.delete(`http://127.0.0.1:8000/comunas${codigo}`)
          .then(responde =>{
            if (responde) {
              Swal.fire('Delete !!','','success')
              this.comunas = responde.data.comunas
            }
          })
        }
      })
    },

    editComuna(id){
      this.$router.push({name: 'EditarComuna', params :{id: `${id}`}}) 
    },
    newcomuna(){
      this.$router.push({nema: 'NewComuna'})
    }
  },
  mounted(){
    axios
      .get('http://127.0.0.1:8000/api/comunas')
      .then(response=> (this.comunas= response.data.comunas.data))
  }
};
</script>
