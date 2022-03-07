<template>
    <div class="accordion" v-bind:id="'accordionShop' + id">
        <div class="accordion-item">
            <h2 class="accordion-header" v-bind:id="'heading' + id">
                <button class="accordion-button" type="button" data-bs-toggle="collapse" v-bind:data-bs-target="'#collapse' + id" aria-expanded="true" v-bind:aria-controls="'collapse' + id">
                    {{ groups }}
                </button>
            </h2>
            <div v-bind:id="'collapse' + id" class="accordion-collapse collapse" v-bind:aria-labelledby="'heading' + id" v-bind:data-bs-parent="'#accordionShop' + id">
                <div class="accordion-body">
                    <div v-for="item in goodsItems" :key="item.G">
                        <ShopItem v-if="item.G == groups" :data="item.B" :dollar="dollar" @addItem="addItem" />
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import ShopItem from './ShopItem.vue'
import shopData from '../../data/data.json'
import goodsData from '../../data/names.json'

export default {
    data() {
        return {
            shopItems: shopData,
            goodsItems: goodsData,
        };
    },
    props: ['groups', 'id', 'G', 'dollar'],
    components: {
        ShopItem,
    },
    methods: {
        addItem(item) {
            return this.$emit('addItem', item);
        }
    }
}
</script>