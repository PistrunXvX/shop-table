<template>
    <div class="container">
        <div v-for="(product, key) in data" :key="product">
            <div v-for ="items in shopItems" :key="items.Goods">
                <div v-for ="item in items.Goods" :key="item">
                    <div v-if="key == item.T" class="row" v-bind:class="changeBg">
                            <div class="col-6">
                                <ul class="list-inline">
                                    <li class="list-inline-item">
                                        <strong v-bind:class="'name-product-' + item.T">{{ product.N }}</strong>
                                    </li>
                                    <li class="list-inline-item">
                                        <small>Количество: {{ item.P }}</small>
                                    </li>
                                </ul>
                            </div>
                            <div class="col-3">
                                <strong v-bind:class="'price-product-' + item.T">Цена: {{ Math.round(item.C * dollar)}}₽</strong>
                            </div> 
                            <div class="col-3">
                                <button @click="addItemCard(item.T)" v-if="item.P > 0" type="button" class="btn btn-sm btn-outline-primary">
                                    В корзину
                                </button>
                                <button v-else type="button" class="btn btn-sm btn-outline-primary" disabled>
                                    В корзину
                                </button>
                            </div> 
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import shopData from '../../data/data.json'
import goodsData from '../../data/names.json'

export default {
    data() {
        return {
            shopItems: shopData,
            goodsItems: goodsData,
            lastDollar: this.dollar,
        }
    },
    props: ['data', 'dollar'],
    methods: {
        addItemCard(id) {
            let item = new Map ([
                ['name', 'name'],
                ['price', 0],
            ]);
            let name = document.querySelector('.name-product-' + id).innerHTML;
            let price = Number(document.querySelector('.price-product-' + id).innerHTML.replace(/[^0-9,\s]/g,""));
            item.set('name', name);
            item.set('price', price);
            return this.$emit('addItem', item);
        }
    },
    computed: {
        changeBg() {
            if (this.dollar == this.lastDollar) {
                return 'default';
            } else if (this.dollar > this.lastDollar) {
                return 'bg-red';
            } else {
                return 'bg-green';
            }
        }
    }
}
</script>

<style scoped>
    .bg-green{
        background-color: #75B798;
    }
    .bg-red {
        background-color: #F1AEB5;
    }
</style>