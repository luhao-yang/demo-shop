<template>
<form class="column is-4" method="post" @submit.prevent="add_to_cart()">
    <h2 class="title is-4" v-if="product.variant_title">{{product.variant_title}}</h2>
    <div class="content">
        <strong>Price</strong>: {{product.special_price ? product.special_price.toDollar() : product.price.toDollar()}} <template v-if="product.special_price"><strike>{{product.price.toDollar()}}</strike>, {{product.discount_rate}}%</template>
    </div>
    <div class="field">
        <div class="control">
            <input type="number" v-model="qty" class="input" />
        </div>
    </div>
    <div class="field">
        <button type="submit" class="button is-primary">add to cart</button>
    </div>
</form>
</template>

<script>
export default {
    name        :   'AddToCart',
    props       :   [ 'product' ],
    data()
    {
        return {
            qty :   1
        };
    },
    methods     :   {
        add_to_cart()
        {
            let data    =   new FormData();
            data.append('id', this.product.id);
            data.append('class', this.product.class);
            data.append('qty', this.qty);

            this.$cart.dispatch('add_to_cart', data).then(() => {
                alert('Product added! Now go to "Cart"');
            });
        }
    }
}
</script>
