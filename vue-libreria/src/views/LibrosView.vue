<script>
import axios from 'axios';
import {ref, onMounted} from 'vue';

export default {
    setup() {
        const libros = ref([]);

        const listarLibros = async()=>{
            try {
                const response = await axios.get('http://localhost:3000/libros');
                libros.value = response.data;
                console.log(libros.value)
            } catch (error) {
                console.log("Error al leer los libros desde el endpoint", error)
            }
        };

        const eliminarLibro = async (id, titulo) => {
            const confirmDelete = window.confirm(`¿Estás seguro de que deseas eliminar el libro "${titulo}"?`);
            if (confirmDelete) {
                try {
                    await axios.delete(`http://localhost:3000/libros/${id}`);
                    // Actualiza la lista de libros después de eliminar el libro escogido
                    listarLibros();
                } catch (error) {
                    console.log(`Error al eliminar el libro "${titulo}"`, error);
                }
            }
            
        };

        onMounted(() => {
            listarLibros();
        });

        return {
            libros,
            listarLibros,
            eliminarLibro
        };
    }
}
</script>

<template>
    <main>
        <table>
            <thead>
                <tr>
                    <th>Id</th>
                    <th>Título</th>
                    <th>Autor</th>
                    <th>ISBN</th>
                    <th>Género</th>
                    <th>Precio</th>
                    <th>Disponibilidad</th>
                    <th>Acciones</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="libro in libros" :key="libro.id">
                    <td class="alinear">{{ libro.id }}</td>
                    <td>{{ libro.titulo }}</td>
                    <td>{{ libro.autor }}</td>
                    <td>{{ libro.ISBN }}</td>
                    <td>{{ libro.genero }}</td>
                    <td class="alinear">{{ libro.precio }}</td>
                    <td>{{ libro.disponibilidad }}</td>
                    <td class="botones">
                        <button class="btn eliminar" @click="eliminarLibro(libro.id,libro.titulo)">
                            Eliminar
                        </button>
                        <RouterLink class="btn editar" :to="{ path:'editarLibro/' + libro.id }">
                            Editar
                        </RouterLink>
                    </td>
                </tr>
            </tbody>
        </table>
    </main>
</template>

<style scoped>
    table {
        border-collapse: collapse;
        margin: 25px auto;
        box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
    }

    td, th {
        border: 1px solid #000;
        padding: 10px;
    }

    th {
        background-color: #e2e2e2;
    }

    .alinear {
        text-align: center;
    }

    .botones {
        display: flex;
        justify-content: space-around;
        align-items: center;
        border: 1px solid #a09d9d;
    }

    .btn {
        background-color: transparent;
        border: none;
        padding: 10px 15px;
        text-decoration: none;
        font-family: "Wix Madefor Text", sans-serif;
        color: #000;
        font-size: 1em;
        border-radius: 5px;
        cursor: pointer;
        transition: background-color 0.3s ease in-out;
        margin: 5px;
    }

    .eliminar {
        background-color: red;
        color: #fff;
    }

    .eliminar:hover {
        background-color: rgb(187, 0, 0);
    }

    .editar {
        background-color: orange;
        color: #fff;
    }

    .editar:hover {
        background-color: rgb(207, 135, 0);
    }
</style>