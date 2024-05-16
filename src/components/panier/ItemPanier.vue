<template>
    <div class="cart-item">
        <img v-bind:src="product.image">
        <div class="cart-item-info">
            <div class="cart-item-name">{{ product.name }}</div>
            <!-- ** Exercice 1.5 : format du prix ** -->
            <div class="cart-item-price">{{ product.price }}</div>
            <div class="cart-item-quantity"><span>Quantité:</span>
                <input type="number" class="quantity" v-bind:value="quantity"
                    v-on:input="emitChangeQuantity($event.target.value)" min="1" />
            </div>
            <!-- ** Exercice 1.5 : format du prix ** -->
            <div class="cart-item-total">Total: {{ quantity * product.price }}</div>
        </div>
        <div class="cart-item-remove">
            <button v-on:click="$emit('remove', product.id)">Retirer</button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        product: Object,
        quantity: Number
    },
    emits: ['changeQuantity', 'remove'],
    methods: {
        emitChangeQuantity(qty) {
            const qtyNum = +qty
            this.$emit('changeQuantity', this.product.id, qtyNum);
        }
    }
}
</script>

<style scoped>
.cart-item {
    margin-bottom: 10px;
    border: 1px solid black;
    padding: 10px;
    overflow: hidden;
    clear: both;
}

.cart-item img {
    float: left;
    margin-right: 10px;
    width: 50px;
    object-fit: cover;
}

.cart-item-info {
    float: left;
    width: 60%;
}

.cart-item-name {
    font-weight: bold;
    font-size: 1.1em;
    margin-bottom: 5px;
}

.cart-item-price {
    font-weight: bold;
    font-size: 1.1em;
    color: green;
}

.cart-item-remove {
    float: right;
    width: 40%;
    text-align: right;
    font-size: 1.1em;
    line-height: 2em;
}

.quantity {
    width: 50px;
    text-align: center;
    margin-right: 10px;
}
</style>
