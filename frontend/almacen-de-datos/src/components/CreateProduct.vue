<template>
    <form @submit.prevent="handleSubmit">
    <h2> Crear Productos</h2>
    <div>
        <label for="profuct-name">Nombre del producto:</label>
        <input type="text" v-model="product.product_name" id="product-name" required>
    </div>
    <div>
        <label for="description">Descripcion del producto:</label>
        <input type="text" v-model="product.product_description" id="description" required>
    </div>
    <button type="submit">Crear Producto</button>
    </form>
</template>

<script>
import axios from 'axios';

export default {
    name: 'CreateProduct',
    data() {
    return {
        product: {
        product_name: '',
        product_description: ''
        }
    };
    },
    methods: {
    resetForm() {
        this.product = { product_name: '', product_description: ''};
    },
    async handleSubmit() {
        try {
        const response = await axios.post('http://localhost:4000/api/product', this.product);
        console.log(response.data);
          this.$emit('productCreated'); // Emitir un evento para informar que se ha creado un usuario
          this.resetForm(); // Limpiar el formulario
        } catch (error) {
        console.error('There was an error creating the product!', error);
        }
    }
    }
};
</script>
