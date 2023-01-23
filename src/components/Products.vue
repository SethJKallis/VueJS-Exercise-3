<template>
        <button v-on:click="toggleLoader()">Toggle Loader</button>

<div v-if="loadingItems" class="spinnerContainer">
    <spinnerComponent/>
</div>

<div v-else class="productsComponentContainer">
    <div class="card border border-5" v-for="product in products" v-bind:key="product">
<img class="card-img-top" v-bind:src="product.url" v-bind:alt="product.name" width="200">
<div class="card-body">
  <h5 class="card-title">{{ product.name }}</h5>
<p class="card-text">R{{ product.price }}</p>
<a href="#" class="btn btn-primary" v-on:click="purchaseBtn(product)" v-if="cart.includes(product.id)">Purchase</a>
<!-- <a href="#" class="btn btn-primary">Purchased</a> -->
</div>
</div>
</div>
  
    
</template>

<script>
let cart = []
let products = [{
    id: 1,
    name: "Assassin's Creed",
    price: 50,
    description: 'First Installment',
    url: 'https://i.postimg.cc/Y9Jm3Mmm/Assassin-s-Creed.jpg'
},
{
    id: 2,
    name: "Assassin's Creed II",
    price: 75,
    description: 'Second Installment',
    url: 'https://i.postimg.cc/Vk5LfNPm/AC-2.jpg'
},
{
    id: 3,
    name: "Assassin's Creed III",
    price: 100,
    description: 'Third Installment',
    url: 'https://i.postimg.cc/3xVB65pY/Assassin-s-Creed-III-Game-Cover.jpg'
},
{
    id: 4,
    name: "Assassin's Creed IV",
    price: 125,
    description: 'Fourth Installment',
    url: 'https://i.postimg.cc/jStwS8bP/Assassin-s-Creed-IV-Black-Flag-cover.jpg'
},
{
    id: 5,
    name: "Assassin's Creed Brotherhood",
    price: 150,
    description: 'Spin Off',
    url: 'https://i.postimg.cc/qMc4qjmc/AC-Brother-Hood.webp'
}
]
localStorage.setItem('products', JSON.stringify(products))

import spinnerComponent from './Spinner.vue'

export default{
    name: 'productsComponent',
    components:{
        spinnerComponent
    },
    data: function () {
        return{
            products: JSON.parse(localStorage.getItem('products')),
            loadingItems: true,
        } 
    },
    
    // DOM updates asynchronously. Collects components and then creates a single batch to update the DOM. Changes are not immediately rendered on the DOM
    
    // this.$nextTick() executes code AFTER changes have been made to the DOM
    mounted() {
        // this.$nextTick(
            //     function(){
                //     this.loadingItems = false
                // })
                // this.loadingItems = true;

                // setTimeout TAKE A CALLBACK AS AN ARGUMENT(DECLARING THE FUNCTION AS THE CALLBACK CREATES PROBLEMS, SO USE ARROW FUNCTION)
                setTimeout(() => {
                    this.loadingItems = false
                }, 1000)
    },

    methods:{
        toggleLoader(){
            this.loadingItems = !this.loadingItems
    },
    purchaseBtn(product){
        alert(`You've Purchased ${product.name} for R${product.price}`);
        cart.push(product.id)
        console.log(cart)
    }
    } 
}
</script>

<style scoped>

img{
    display: block;
    width: 100%;
    height: 75%;
}
.productsComponentContainer{
    display: grid;
    grid-template-columns: repeat(3,1fr);
    gap: 1rem;

}
.spinnerContainer{
margin-top: 150px;
}
</style>