<template>
    <div>
        <section v-if="error">
            {{ error.message }}
        </section>
        <section v-else>
            <div v-if="loading">
                <h2 class="loading">Loading</h2>
            </div>
            <div v-else>
                <h2>{{ product.name }}</h2>
                <img :src="product.imageUrl ? product.imageUrl : 'https://picsum.photos/250/150'" width="200"
                    style="float:right" />
                <h3>{{ product.description }}</h3>
                <p>Price: {{ product.price }}</p>
                <p>Fixed price? {{ product.fixedPrice }}</p>
                <p>Discontinued? {{ product.discontinued }}</p>
                <p>Modified date: {{ product.modifiedDate }}</p>
            </div>
        </section>
    </div>
</template>

<script>
import { mapState, mapActions } from 'vuex'

export default {
    props: {
        id: {
            type: Number,
            required: true
        }
    },
    data() {
        return {
            error: null
        }
    },
    computed: {
        ...mapState(['product', {loading: 'isLoading'}]),
    },
    methods: {
        ...mapActions(['fetchProduct'])
    },
    created() {
        this.fetchProduct(this.id);
    },
}
</script>

<style lang="scss" scoped></style>