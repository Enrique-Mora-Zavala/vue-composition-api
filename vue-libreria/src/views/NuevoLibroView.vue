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
            <button type="submit">Agregar Libro</button>
        </form>
    </main>
</template>

<style>

</style>