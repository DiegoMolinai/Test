<template>
    <div>
        <h1 class="display4 text-center">Listado de Tareas</h1>
        <hr>
        <div class="row">
            <div class="col-lg-8 offset-lg-2">
                <div class="card mt-4">
                    <div class="card-body">
                        <div class="input-group">
                            <input type="text" v-model="tarea" class="form-control form-control-lg" placeholder="Agregar Tarea">
                            <div class="input-group-append">
                                <button v-on:click=agregarTarea() class="btn btn-success btn-lg">Agregar</button>
                            </div>
                        </div>
                        <br>
                        <h5 v-if="listTarea.length == 0">No hay tareas para realizar</h5>
                        <ul class="list-group">
                            <li v-for="(tarea,index) of listTarea" :key="index" class="list-group-item d-flex justify-content-between">
                                <span class="cursor" v-bind:class="{'text-success' : tarea.estado}" v-on:click="editarTarea(tarea,index)">
                                    <i v-bind:class="[tarea.estado ? 'fas fa-check-circle' : 'far fa-circle']"></i>
                                </span>
                                {{ tarea.nombre }}
                                <span class="text-danger cursor" v-on:click="eliminarTarea(index)">
                                    <i class="fal fa-trash-alt"></i>
                                </span>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name:'Tarea',
        data(){
            return{
                tarea:'',
                listTarea:[]
            }
        },
        methods:
        {
            agregarTarea()
            {
                const tarea={
                    nombre:this.tarea,
                    estado:false
                }
                this.listTarea.push(tarea);
                this.tarea = '';
            },
            eliminarTarea(index)
            {
                this.listTarea.splice(index,1);
            },
            editarTarea(tarea,index)
            {
                this.listTarea[index].estado = !tarea.estado;
            }
        }
    }
</script>

<style scoped>
.cursor
{
    cursor:pointer;
}
</style>