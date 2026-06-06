<script>
    import axios from 'axios';
    import { ref, onMounted } from 'vue';
    import { useRoute, useRouter } from 'vue-router';

    export default {
        setup() {
            const router = useRouter();

            const editarLibro = ref({
                titulo: '',
                autor: '',
                ISBN: '',
                genero: '',
                precio: '',
                disponibilidad: ''
            });

            const cargarLibro = async () => {
                const libroId = useRoute().params.id;
                try {
                    const response = await axios.get(`http://localhost:3000/libros/${libroId}`);
                    editarLibro.value = response.data;
                } catch (error) {
                    console.log('Error al cargar el libro', error);
                }
            };

            const actualizarLibro = async () => {
                try {
                    await axios.put(`http://localhost:3000/libros/${libroId}`, editarLibro.value);
                    setTimeout(() => {
                        alert('Libro editado con éxito');
                    }, 500);
                    router.push('/');
                } catch (error) {
                    console.log('Error al editar el libro', error);
                }
            };

            onMounted(() => {
                cargarLibro();
            });

            return {
                editarLibro,
                actualizarLibro,
                cargarLibro
            };
        }
    }
</script>

<template>
    <main>
        <form @submit.prevent="actualizarLibro">
            <div>
                <div>
                    <label for="titulo">Título:</label>
                    <input v-model="editarLibro.titulo" type="text" required placeholder="título">
                </div>
                <div>
                    <label for="autor">Autor:</label>
                    <input v-model="editarLibro.autor" type="text" required placeholder="autor">
                </div>
                <div>
                    <label for="ISBN">ISBN:</label>
                    <input v-model="editarLibro.ISBN" type="text" required placeholder="ISBN">
                </div>
                <div>
                    <label for="genero">Género:</label>
                    <input v-model="editarLibro.genero" type="text" required placeholder="genero">
                </div>
                <div>
                    <label for="precio">Precio:</label>
                    <input v-model="editarLibro.precio" type="text" required placeholder="precio">
                </div>
                <div>
                    <label for="disponibilidad">Disponibilidad:</label>
                    <input v-model="editarLibro.disponibilidad" type="text" required placeholder="disponibilidad">
                </div>
            </div>
            <button type="submit">Guardar cambios</button>
        </form>
    </main>
</template>

<style>

</style>