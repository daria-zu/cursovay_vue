<template>
<section>
  <div class="card" v-for="item in getPhones" :key="item.id">
      <div class="box_img">
        <img :src="require('@/assets/' + item.img)">
      </div>
      <div class="box_text">
        <h2>{{item.name}}</h2>
        <p>{{item.prise}} руб.</p>
        <button @click="shop(item)">Купить</button>
      </div>
      <div class="box_link">
        <router-link class="link" :to="{name:'Card', params: {id: item.id}}">Подробнее -></router-link>
      </div>
  </div>
</section>

    <router-view/>
</template>

<script>
import {mapGetters} from 'vuex';
export default {
    name:'Phone',
    computed: {
        ...mapGetters(['getPhones'])
    },
     methods:{
         shop(item){
            this.$store.commit('addToBasket', {product: item});
        }
    }
}
</script>

<style scoped>
    section{
        display: flex;
        flex-direction: column;
        flex-grow: 1;
    }
    .card{
        height: 105px;
        margin: 1rem;
        background-color: white;
        padding: 1rem;
        flex: 1;
        display: flex;
        border: 2px solid white;
    }
    .box_img{
        width: 30%;
        border: 1px solid transparent
    }
    img{
        width: 100px;
        overflow: hidden;
    }
    .box_text{
        width: 70%;
        padding-left: 5px;
        display: flex;
        flex-direction: column;
    }
    p{
        margin-top: 10px;
    }
    button{
      width: 15%;
      border: 1px solid rgb(29, 28, 28);
      border-radius: 3px;
      background-color: rgb(146, 148, 151);
      color: rgb(29, 28, 28);
      cursor: pointer;
      margin-top: 10px;
   }
   button:focus{
      border: 2px solid #b30000;
   }
     .box_link{
        width: 10%;
       padding-left: 10px;
    }
   .link{
       text-decoration: none;
       color: #151719;
   }
</style>