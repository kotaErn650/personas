<template>
  <div class="container text-start">
    <h class="text-primary fw-bold">
      <div class="card">
        <div class="card-header fw-blod">Comuna</div>
        <div class="car-body">
          <form @submit.prevent="updataComuna">
            <div class="row md-3">
              <label for="comu_codi" class="form-label">codigo</label>
              <div class="inpu-group">
                <div class="input-group-text">
                  <font-awesome-icon icon="building" />
                </div>
                <input
                  type="text"
                  class="form-control"
                  id="comu_nomb"
                  placeholder="Codigo comuna"
                  v-model="Comuna.comu_nomb"
                />
              </div>
            </div>
            <div class="row mb-3">
              <label for="muni_codi" class="form-label">Municipo : </label>
              <div class="input-group">
                <div class="input-group-text">
                  <font-awesome-icon icon="bank" />
                </div>
                <select class="form-select" v-model="Comuna.muni_codi">
                  <option v-for="municipio in municipios" :key="municipio.muni_codi" v-bind:value="municipio.muni_codi">{{ municipio.muni_codi }}</option>
                </select>
              </div>
            </div>
            <button class="btn btn-primary" type="submit">Actualizar</button>
            <button class="btn btn-secundary mx-2" @click="cancelar">
              Cancelar
            </button>
          </form>
        </div>
      </div>
    </h>
  </div>
</template>

<script>

import axios from "axios";
import Swal from "sweetalert2";

export default {
  name: "EditarVomuna",
  data() {
    return {
      Comuna: {
        comu_codi: 0,
        comu_nomb: "",
        muni_codi: 0,
      },
      municipios: [],
    };
  },
  /**
   *
   */
  cancelar() {
    this.$router.push({ name: "Comunas" });
  },
  async updataComuna() {
    const res = await axios.put(
      `http://127.0.0.1:8000/api/comunas/${this.Comuna.comu_codi}`,
      this.Comuna
    );

    if (res.status == 200) {
      this.$router.push({ name: "Comunas" });
      Swal.fire({
        position: "top-end",
        icon: "success",
        title: "Comuna has been Updated",
        showConfirmButton: false,
        timer: 2000,
      });
    }
  },
  mounted() {
    this.Comuna.comu_codi = this.$route.params.id;
    axios
      .get(`http://127.0.0.1:8000/api/comunas/${this.Comuna.comu_codi}`)
      .then(response => {
        this.Comuna = response.data.comuna;
        this.municipios = response.data.municipios;
      });
  }
};
</script>
