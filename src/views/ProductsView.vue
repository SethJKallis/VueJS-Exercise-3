<template>
    <div class="products">
        <h1>Products</h1>
        <productsComponent/>
    </div>
</template>

<script>
import productsComponent from '../components/Products.vue'

export default{
    name: 'productsView',
    components: {
        productsComponent
    }
}
</script>