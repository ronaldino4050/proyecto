<template>
    <div class="container">
       <h1>Tabla de Clientes</h1>
       <table>
        <thead>
            <tr>
                <th>Codigo</th>
                <th>Nombre</th>
                <th>Apellido</th>
                <th>Edad</th>
                <th>Email</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="cliente in cliente" :key="cliente.Codigo">
             <td>{{ cliente.Codigo }}</td>
             <td>{{ cliente.nombre}}</td>
             <td>{{ cliente.apellido }}</td>
             <td>{{ cliente.edad }}</td>
             <td>{{ cliente.email }}</td>
            </tr>

            <router-View/>

        </tbody>
       </table>

    </div>
</template>
<script>
import axios from "axios"
export default{
    data(){
        return{
            clientes:[],
        };
    },

    methods:{
        obtenerclientes(){
            //metodo para obtener la lista de todos los clientes
            axios.get("http://localhost:8080/api/clientes/listar")
            .then ((response)=>{
                this.clientes = response.data;
            })
            .catch((error) =>{
                console.error("Error al ontener clientes:",error);
            });       
         },
    },
    mounted(){
        //llamar al metodo para obtener la lista de clientes al cargar el componente
        this.obtenerclientes();
    },
};

</script>