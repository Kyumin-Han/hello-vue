<template>
    <div class="product">
        <div class="product-image">
            <img :src="image">
        </div>
        <div class="product-info">
            <h1>{{ title }}</h1>
            <p v-if="inStock">In Stock</p>
            <p v-else>Out of Stock</p>
            <!-- <p v-if="inventory > 10">In Stock</p> <p v-else-if="inventory > 0">Almost
            sold out!</p> <p v-else>Out of Stock</p> -->
            <ul>
                <li v-for="(detail, i) in details" :key="i">{{ detail }}</li>
            </ul>
            <div
                v-for="(variant, index) in variants"
                :key="variant.variantId"
                class="color-box"
                :style="{backgroundColor: variant.variantColor}"
                v-on:mouseover="updateProduct(index)">
                <!-- <p v-on:mouseover="updateProduct(variant.variantImage)">{{
                variant.variantColor }}</p> -->
            </div>
            <button
                v-on:click="addToCart"
                :disabled="!inStock"
                :class="{disabledButton: !inStock}">Add to Cart</button>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                brand: "Vue", product: 'Socks', selectedVariant: 0,

                // inventory: 100 inStock: true,
                details: [
                    "80% cotton", "20% polyester", "Gender-neutral"
                ],
                variants: [
                    {
                        variantId: 2234,
                        variantColor: "green",
                        variantImage: require('@/assets/images/socks_green.jpg'),
                        variantQuantity: 10
                    }, {
                        variantId: 2235,
                        variantColor: "blue",
                        variantImage: require('@/assets/images/socks_blue.jpg'),
                        variantQuantity: 0
                    }
                ]
            }
        },
        methods: {
            addToCart() {
                this.$emit('add-to-cart', this.variants[this.selectedVariant].variantId)
            },
            updateProduct(index) {
                this.selectedVariant = index
            }
        },
        computed: {
            title() {
                return this.brand + ' ' + this.product
            },
            image() {
                return this
                    .variants[this.selectedVariant]
                    .variantImage
            },
            inStock() {
                return this
                    .variants[this.selectedVariant]
                    .variantQuantity
            }
        }
    }
</script>