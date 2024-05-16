<template>
    <div id="cart-pane">
        <h2>Panier</h2>
        <div id="cart-items">
            <ItemPanier v-for="cartitem in cartWithProducts" :key="cartitem.product.id" v-bind="cartitem"
                @change-quantity="(id, qty) => $emit('changeQuantity', id, qty)" @remove="(id) => $emit('remove', id)" />
        </div>
        <div id="cart-summary">
            <!-- ** Exercice 1.3 : modifier afin d'utiliser une propriété calculée ** -->
            <!-- ** Exercice 1.5 : format du prix ** -->
            Total: <span id="cart-total">{{ calculateTotal() }}</span>
        </div>
        <button>Passer à la caisse</button>
    </div>
</template>

<script>
import ItemPanier from './ItemPanier.vue';
export default {
    components: {
        ItemPanier: ItemPanier
    },
    data() {
        return {
            // ** Exercice 1.1 : remplacer par un inject de la donnée 'products' disponible dans App.vue **
            products: []
        };
    },
    props: {
        cart: Array
    },
    emits: ['changeQuantity', 'remove'],
    computed: {
        cartWithProducts() {
            return this.cart.map(cartitem => {
                let product = this.findProduct(cartitem.productId);
                if (!product) {
                    // produit introuvable, instancier un produit bidon
                    // avec le même id
                    product = {
                        id: cartitem.productId,
                        name: 'Produit avec id \'' + cartitem.productId + '\' introuvable!',
                        price: 0,
                        desc: 'PRODUIT INTROUVABLE!',
                        image: 'products/bidon.jpg'
                    }
                }

                return {
                    product: product,
                    quantity: cartitem.quantity
                };
            });
        }
    },
    methods: {
        findProduct: function (productId) {
            return this.products.find(p => p.id === productId);
        },
        calculateTotal: function () {
            let total = 0;
            this.cartWithProducts.forEach((item) => {
                total = total + item.quantity * item.product.price;
            });

            return total;
        }
    }
}
</script>

<style scoped>
#cart-pane {
    flex-basis: 30%;
    border: 1px solid black;
    padding: 10px;
}
</style>
