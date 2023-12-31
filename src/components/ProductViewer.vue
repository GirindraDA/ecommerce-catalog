<script>
import LoadingPlaceholder from './LoadingPlaceholder.vue';
import ProductNotAvailable from './ProductNotAvailable.vue';

export default {
    name: 'ProductViewer',
    components: { LoadingPlaceholder, ProductNotAvailable },
    data() {
        return {
            product: {},
            currentId: 1,
            fetchStatus: false,
            theme: {},
            isAvailable: true,
            availableCategories: ["men's clothing", "women's clothing"],
        };
    },
    created() {
        this.fetchStatus = true;
        this.fetchProducts();
    },
    methods: {
        async fetchProducts() {
            const res = await fetch(
                `https://fakestoreapi.com/products/${this.currentId}`
            );
            const productData = await res.json();
            this.product = productData;
            this.changeTheme();

            const { category } = this.product;

            if (
                category === this.availableCategories[0] ||
                category === this.availableCategories[1]
            ) {
                this.isAvailable = true;
            } else {
                this.isAvailable = false;
            }

            this.fetchStatus = false;
        },
        fetchNextProduct() {
            this.fetchStatus = true;
            this.currentId === 20 ? (this.currentId = 1) : ++this.currentId;
            this.fetchProducts();
        },
        changeTheme() {
            if (this.product.category === "men's clothing") {
                this.theme = {
                    bg: 'bg-men',
                    text: 'text-men',
                    rating: 'circle-men',
                    filled: 'filled-men',
                    buttonBuy: 'btn-buy-men',
                    buttonNext: 'btn-next-men',
                };
            } else if (this.product.category === "women's clothing") {
                this.theme = {
                    bg: 'bg-women',
                    text: 'text-women',
                    rating: 'circle-women',
                    filled: 'filled-women',
                    buttonBuy: 'btn-buy-women',
                    buttonNext: 'btn-next-women',
                };
            } else {
                this.theme = {
                    bg: 'bg-default',
                };
            }
        }
    },
};
</script>

<template>
    <div class="bg" :class="theme.bg"></div>
    <section class="wrapper">
        <div class="product-box">
            <LoadingPlaceholder v-if="fetchStatus" />
            <ProductNotAvailable
                v-if="!fetchStatus && !isAvailable"
                :nextFunction="fetchNextProduct"
            />
            <div v-if="!fetchStatus && isAvailable" class="product-wrapper">
                <div class="img-wrapper">
                    <img :src="product.image" :alt="product.title" />
                </div>
                <div class="wrapper-col">
                    <div class="detail-wrapper">
                        <h1 :class="theme.text">{{ product.title }}</h1>

                        <div>
                            <div class="category">
                                <span>{{ product.category }}</span>
                                <div class="rating">
                                    <span>{{ product?.rating?.rate }}/5</span>
                                    <div class="rating-circle">
                                        <div
                                            v-for="index in 5"
                                            :key="index"
                                            class="circle"
                                            :class="[
                                                theme.rating,
                                                {
                                                    [theme.filled]:
                                                        index <=
                                                        product?.rating?.rate,
                                                },
                                            ]"
                                        ></div>
                                    </div>
                                </div>
                            </div>
                            <hr />
                        </div>

                        <p>{{ product.description }}</p>
                    </div>
                    <div class="detail-wrapper">
                        <div>
                            <hr />
                            <span :class="theme.text" class="price"
                                >${{ product.price }}</span
                            >
                        </div>
                        <div class="btns-wrapper">
                            <button :class="theme.buttonBuy">Buy Now</button>
                            <button
                                :class="theme.buttonNext"
                                @click="fetchNextProduct"
                            >
                                Next Product
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>
