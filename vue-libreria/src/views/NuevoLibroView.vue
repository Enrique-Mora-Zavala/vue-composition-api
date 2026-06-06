<script>
    import { ref, onMounted } from 'vue';
    import axios from 'axios';
    export default {
        setup() {
            const nuevoLibro = ref({
                titulo: '',
                autor: '',
                ISBN: '',
                genero: '',
                precio: '',
                disponibilidad: ''
            });

            const agregarLibro = async () => {
                try {
                    const response = await axios.post('http://localhost:3000/libros', nuevoLibro.value);

                    setTimeout(() => {
                        alert('Libro agregado con éxito');
                    }, 200);
                    
                    nuevoLibro.value.titulo= '',
                    nuevoLibro.value.autor= '',
                    nuevoLibro.value.ISBN= '',
                    nuevoLibro.value.genero= '',
                    nuevoLibro.value.precio= '',
                    nuevoLibro.value.disponibilidad= ''

                    console.log('Libro agregado con éxito', response.data);

                } catch (error) {
                    console.log('Error al agregar el libro', error);
                }
            };

            return {
                nuevoLibro,
                agregarLibro
            };
        }
    }
</script>

<template>
    <main>
        <form @submit.prevent="agregarLibro">
            <div>
                <div>
                    <label for="titulo">Título:</label>
                    <input v-model="nuevoLibro.titulo" type="text" required placeholder="título">
                </div>
                <div>
                    <label for="autor">Autor:</label>
                    <input v-model="nuevoLibro.autor" type="text" required placeholder="autor">
                </div>
                <div>
                    <label for="ISBN">ISBN:</label>
                    <input v-model="nuevoLibro.ISBN" type="text" required placeholder="ISBN">
                </div>
                <div>
                    <label for="genero">Género:</label>
                    <input v-model="nuevoLibro.genero" type="text" required placeholder="genero">
                </div>
                <div>
                    <label for="precio">Precio:</label>
                    <input v-model="nuevoLibro.precio" type="text" required placeholder="precio">
                </div>
                <div>
                    <label for="disponibilidad">Disponibilidad:</label>
                    <input v-model="nuevoLibro.disponibilidad" type="text" required placeholder="disponibilidad">
                </div>
            </div>
            <button class="btn enviar" type="submit">Agregar Libro</button>
        </form>
    </main>
</template>

<style scoped>
    form {
        width: 90%;
        margin: 25px auto;
        padding: 20px;
        border: solid 1px #000;
        box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
    }

    label {
        font-weight: bold;
        margin-bottom: 5px;
        display: block;
        font-size: 1rem;
    }

    input {
        width: 100%;
        padding: 5px;
        border: 1px solid #000;
        margin-bottom: 15px;
        font-family: "Wix Madefor Text", sans-serif;
        font-size: 1rem;
    }

    input:focus {
        outline: none;
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
        width: 100%;
    }

    .enviar {
        background-color: green;
        color: #fff;
    }

    .enviar:hover {
        background-color: rgb(1, 98, 1);
    }
</style>