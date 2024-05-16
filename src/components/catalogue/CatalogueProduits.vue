<template>
    <div id="product-list">
        <h2>Catalogue de produits</h2>
        <ItemCatalogue v-for="product in products" :key="product.id" :id="product.id" :name="product.name"
            :price="product.price" :desc="product.desc" :image="product.image" />
    </div>
</template>

<script>
import ItemCatalogue from './ItemCatalogue.vue';
export default {
    components: {
        ItemCatalogue: ItemCatalogue
    },
    data() {
        return {
            // Le catalogue des produits disponibles:

            // ** Exercice 1.1 : remplacer par un inject de la donnée 'products' disponible dans App.vue **
            products: [
                {
                    id: 'chaise',
                    name: 'Chaise verte',
                    price: 29.99,
                    desc: 'Une chaise en plastique, de couleur verte.',
                    image: 'products/chaise.jpg'
                }
            ]

        };
    }
}
</script>

<style scoped>
#product-list {
    flex-basis: 70%;
    margin-right: 20px;
    border: 1px solid black;
    padding: 10px;
}
</style>
