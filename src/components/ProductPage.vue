<template>
    <div id="app">
        <div class="nav-bar"></div>
        <div class="cart">
            <p>Cart{{ cart.length }}</p>
        </div>
        <product @add-to-cart="addToCart"></product>
        <Reply></reply>
    </div>
</template>

<script>
    import Product from './Product.vue';
    import Reply from './Reply.vue';

    export default {
        name: 'ProductPage',
        components: {
            Product,
            Reply
        },
        data() {
            return {
                cart: [],
                user: null,
                comment: null,
                messages: []
            }
        },
        methods:{
            addToCart(variantId){
                this.cart.push(variantId)
            },
            save() {
                const message={
                    user: this.user,
                    comment: this.comment
                };

                this.messages.unshift(message);
                this.user=null;
                this.comment=null;
            }
        }
    }
</script>