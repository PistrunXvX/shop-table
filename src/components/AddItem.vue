<template>
    <tr v-for="(i, index) in countItems" :key="index" v-bind:class="'item-' + index">
        <th scope="col">{{ dataNames.get('name' + index) }}</th>
        <th>1</th> 
        <th class="price">{{ dataPrice.get('price' + index) }}₽</th>
        <th>
            <button @click="deletItem(index)" type="button" class="btn btn-sm btn-outline-danger">
                Удалить
            </button>
        </th>
    </tr>
    <div class="d-flex">
        Итоговая сумма: {{ sumAllPosition }}₽
    </div>
</template>

<script>
 /* eslint-disable */
export default {
    data() {
        return {
            sum: 0,
        };
    },
    props: ['dataNames','dataPrice', 'countItems'],
    methods: {
        deletItem(index, price) {
            let deletItem = document.querySelector('.item-' + index);
            this.dataPrice.delete('price' + index);
            console.log(price);
            deletItem.remove();
        }
    },
    computed: {
        sumAllPosition() {
            this.sum = 0;
            for (let price of this.dataPrice.values()) {
                this.sum += price;
            }
            return this.sum;
        }
    }
}
</script>