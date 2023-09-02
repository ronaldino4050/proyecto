<template>
    <div class="container">
        <h1>formulario de cliente</h1>
        <form id="cliente-form" @submit.prevent="guardar">
            <div class="form-group">
                <label for="codigo">codigo:</label>
                <input type="text" id="codigo" name="codigo" required v-model="codigo"/>
            </div>
            <div class="form-group">
                <label for="nombre">nombre:</label>
                <input type="text" id="nombre" name="nombre" required v-model="nombre"/>
            </div>
            <div class="form-group">
                <label for="apellido">apellido:</label>
                <input type="text" id="apellido" name="apellido" required v-model="apellido"/>
            </div>
            <div class="form-group">
                <label for="edad">edad:</label>
                <input type="text" id="edad" name="edad" required v-model="edad"/>
            </div>
            <button type="submit" id="guardar" name="guardar">Guardar</button><br/>
            <button type="button" id="eliminar" name="eliminar" @click="eliminar">Eliminar</button><br/>
            <button type="button" id="actualizar" name="actulizar" @click="actualizar">Actualizar</button> <br/>
            <button type="button" id="consultar" name="consultar" @click="eliminar" >Eliminar</button><br/>
        </form>

    </div>

</template>
<script>
import axios from "axios"
export default{
    data(){

        return{
            codigo:"",
            nombre :"",
            apellido :"",
            edad :null,
            email :"",
        };
    },
    methods: {
        guardar(){

            axios
            .post("http://localhost:8080/api/clientes",{
                codigo: this.codigo,
                nombre: this.nombre,
                apellido: this.apellido,
                edad: this.edad,
                email: this.email,

            })
            .then((response)=>{
                console.log("cliente registrado con exito:", response.data);
                alert("exito");
                this.codigo = "";
                this.nombre = "";
                this.apellido = "";
                this.edad = "";
                this.email = "";
            })
            .catch ((error)=>{
                console.error("Error al registrar cliente:",error);
            });
        },

        consultar (){
            axios
            .get('http://localhost:8080/api/clientes/'+this.codigo)
            .then((response)=>{
                // actualizar los campos del fromulario con los datos del cliente consultado
                this.nombre = response.data.nombre;
                this.apellido = response.data.apellido;
                this.edad = response.data.edad;
            })
            .catch ((error)=>{
                console.error("error al consultar cliente:",error);
            });

        },
        actualizar (){
            axios
            .put("http://localhost:8080/api/clientes/actualizar/"+this.codigo,{
                codigo:this.codigo,
                nombre:this.nombre,
                apellido:this.apellido,
                edad:this.edad,
                email: this.email,
            })
            .then((response)=>{
                console.log("cliente actualizado con exito", response.data);
            })
            .catch((error)=>{
                console.error("error alactualizar cliente:", error);
            });

        },
        eliminar(){
            axios
            .delete("http://localhost:8080/api/clientes/"+this.codigo)
            .then(()=>{
                console.log("clienteeliminado con exito");
                //limpiar los campos del formulario despues de elminar
                this.codigo0="";
                this.nombre= "";
                this.apellido= "";
                this.edad= null;
                this.email ="";
            })
            .catch((error)=>{
                console.error("erro al eliminar cliente:",error)
            });
        },

        
    },

};

</script>