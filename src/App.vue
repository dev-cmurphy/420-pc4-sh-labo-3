<template>
    <div class="container">
        <CatalogueProduits />
        <PanierProduits :cart="cart" @change-quantity="changeQuantity" @remove="removeFromCart" />
    </div>
    <button @click="ajouterProduitBidon()">Ajout produit bidon</button>
</template>

<script>
import { computed } from 'vue';
import CatalogueProduits from './components/catalogue/CatalogueProduits.vue';
import PanierProduits from './components/panier/PanierProduits.vue';

import produitsImport from './Produits';

export default {
    components: {
        CatalogueProduits: CatalogueProduits,
        PanierProduits: PanierProduits
    },
    data: function () {
        return {
            // Le catalogue de produit (depuis l'import d'un autre fichier):
            products: produitsImport,
            // Les produits ajoutés au panier, avec leur quantité:
            cart: [
                {
                    productId: 'plante',
                    quantity: 1,
                },
                {
                    productId: 'panier',
                    quantity: 2
                }
            ]
        };
    },
    methods: {
        addToCart: function (productId) {
            let existingItem = null;
            this.cart.forEach(item => {
                if (item.productId === productId) {
                    existingItem = item;
                    existingItem.quantity = existingItem.quantity + 1;
                }
            });

            if (existingItem === null) {
                // Le nouveau cartItem contient uniquement l'identifiant (id) du produit
                // afin d'éviter de dupliquer tous les champs. La logique dans le component
                // PanierProduits s'occupera de récupérer le produit correspondant du catalogue.
                const cartItem = {
                    productId: productId,
                    quantity: 1 // on initialise la quantité à 1
                };

                this.cart.push(cartItem);
            }
        },
        removeFromCart: function (productId) {
            this.cart.forEach((item, idx) => {
                if (item.productId === productId) {
                    this.cart.splice(idx, 1);
                }
            });
        },
        changeQuantity: function (productId, newQuantity) {
            const cartItem = this.cart.find(c => c.productId === productId);
            if (cartItem) {
                if (newQuantity < 1) {
                    cartItem.quantity = 1;
                } else {
                    cartItem.quantity = newQuantity;
                }
            }
        },
        ajouterProduitBidon: function () {
            // ** Exercice 1.4 : expliquer pourquoi cette fonction ne donne pas le résultat voulu
            // (expliquez dans un commentaire ici) et corrigez-la **

            const produitBidon = {
                id: 'bidon',
                name: 'Bidon vert',
                price: 99.99,
                desc: 'Un produit bidon qui est littéralement un bidon',
                image: 'products/bidon.jpg',
                longDesc: "C'est bidonnant."
            };

            if (!produitsImport.find(p => p.id === produitBidon.id)) {
                console.log("ajout bidon");
                produitsImport.push(produitBidon);
            }
        }
    }
}
</script>