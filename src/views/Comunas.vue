<template>
    <div class="container">
        <h1>Listado de comunas</h1>
        <table class="table">
            <thead>
                <tr>
                    <th scope="col">#</th>
                    <th scope="col">Code</th>
                    <th scope="col">Name</th>
                    <th scope="col">Municipality</th>
                </tr>
            </thead>
        </table>
        <tbody>
            <tr v-f="(comuna, index)in comunas" :key="index">
                <th scope="row">{{ index+1 }}</th>
                <th >{{comuna.comu_codi }}</th>
                <th >{{comuna.comu_nomb  }}</th>
                <th >{{comuna.muni_nomb }}</th>
            </tr>
        </tbody>

    </div>
</template>

<script>
import axios from 'axios'

export default{

    name: 'Comuna',
    date(){
        return{
            comunas:[]
        }
    },
    mounted(){
        axios
        .get('http://127.0.0.1:8000/api/comunas')
        .then(respnse => (this.comunas = response.data.comunas))
    },

}

</script>