<template>
    <div class="product">
        <img v-bind:src="image" />
        <div class="product-info">
            <div class="product-name">{{ name }}</div>
            <!-- ** Exercice 1.5 : format du prix ** -->
            <div class="product-price">{{ price }}</div>
            <div class="product-description">{{ desc }}</div>
        </div>
        <div class="product-add-to-cart">
            <!-- ** Exercice 1.2 : injecter et appeler la fonction permettant d'ajouter un item au panier ** -->
            <button>Ajouter au panier</button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        id: String,
        name: String,
        price: Number,
        desc: String,
        image: String
    }
}
</script>

<style scoped>
.product {
    margin-bottom: 20px;
    border: 1px solid black;
    padding: 10px;
    overflow: hidden;
    clear: both;
}

.product img {
    float: left;
    margin-right: 10px;
    width: 100px;
    object-fit: cover;
}

.product-info {
    float: left;
    width: 60%;
}

.product-name {
    font-weight: bold;
    font-size: 1.2em;
    margin-bottom: 5px;
}

.product-price {
    font-weight: bold;
    font-size: 1.2em;
    color: green;
}

.product-description {
    margin-top: 5px;
    font-size: 0.9em;
    color: #666;
}

.product-add-to-cart {
    float: right;
    width: 40%;
    text-align: right;
    font-size: 1.2em;
    line-height: 2em;
}
</style>
