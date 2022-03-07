<template>
  <div class="container-fluid">
     <nav class="navbar navbar-light bg-light">
        <h1>ShopTable</h1>
        <span class="navbar-text">
            <label for="dollar" class="form-label">Ваш курс доллара {{dollar}}</label>
            <input type="number" class="form-control" id="dollar" aria-describedby="dollarHelp" min="100" max="200" v-model="dollar">
            <div id="dollarHelp" class="form-text">Крутите рубль как хотите! </div>
        </span>
        <div class="d-flex">
           <button type="button" class="btn btn-light" data-bs-toggle="modal" data-bs-target="#Modal">
                <img data-bs-toggle="modal" data-bs-target="#Modal" src="./components/icons/cart.svg" alt="" width="50" height="50" class="d-inline-block align-text-top">
            </button>
        </div>
    </nav>
    <div class="modal fade" id="Modal" tabindex="-1" aria-labelledby="ModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="ModalLabel">Корзина</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <table class="table table-hover">
                        <thead>
                            <tr>
                                <th scope="col"><small>Наименование товара и описание</small></th>
                                <th scope="col"><small>Количество</small></th>
                                <th scope="col"><small>Цена</small></th>
                                <th></th>
                            </tr>
                        </thead>
                        <tbody>
                            <AddItem :dataNames="itemsName" :dataPrice="itemsPrice" :countItems="countItems" />
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
  </div>
  <div class="container">
    <div class="row">
      <div class="col-12 col-md-6" v-for="item in goodsItems" :key="item">
          <TableShop :groups="item.G" :id="count++" :dollar="dollar" @addItem="addItemToCard"/>
      </div>
    </div>
  </div>
</template>

<script>
import TableShop from './components/TableShop.vue'
import AddItem from './components/AddItem.vue'
import shopData from '../data/data.json'
import goodsData from '../data/names.json'

export default {
  components: {
    TableShop,
    AddItem,
  },
  data() {
    return {
       shopItems: shopData,
       goodsItems: goodsData,
       count: 0,
       dollar: 150,
      //  items: [
      //    ['name'],
      //    ['price'],
      //  ],
      itemsName: new Map ([
      ]),
      itemsPrice: new Map ([
      ]),
       priceItem: 0,
       nameItem: '',
       countItems: 0,

    };
  },
  mounted: function() {
     this.updateDollar();
  },
  methods: {
    addItemToCard(item) {
      // this.nameItem = item.get('name');
      // this.priceItem = item.get('price');
      this.itemsName.set('name' + this.countItems, item.get('name'));
      this.itemsPrice.set('price' + this.countItems, item.get('price'));
      this.countItems++;
      // return this.items;
    },
    updateDollar() {
      setInterval(function(){
        this.dollar = Math.floor(Math.random() * (200 - 100 +1)) + 100;
      }.bind(this), 15000);
    }
  },
  // computed: {
  //   addItemToArr() {
  //     this.items[0][this.countItems] = this.nameItem;
  //     this.items[1][this.countItems] = this.priceItem;
  //     this.countItems++;
  //     // console.log(this.items);
  //     // this.items.set('name', this.nameItem);
  //     // this.items.set('price', this.priceItem);
  //   }
  // }
}
</script>

<style>
/* @import './assets/base.css'; */

/* #app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;

  font-weight: normal;
}

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
  }

  #app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
  }

  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .logo {
    margin: 0 2rem 0 0;
  }
}
*/
</style>
