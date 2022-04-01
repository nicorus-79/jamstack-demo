<template>
  <div>
    <div>
      <div>
        <input v-model="zipcode" />
        <button @click="getProductsData(zipcode)">郵便番号情報取得</button>
        <button @click="showResult=!showResult">{{showResult ? "閉じる" : "開く"}}</button>
        <dialog v-if="showResult" :class="$style.dialog" open>
          {{apiResult}}
        </dialog>
        <h1>写真一覧</h1>
        <ul v-for="item in items" :key="item.id">
          <nuxt-link :to="'/items/'+item.id"><img :src="item.image.url" /></nuxt-link>
        </ul>
      </div>
    </div>
  </div>
</template>
<script>
 export default {
  data () {
    return {
      items: [],
      apiResult: "",
      showResult: true,
      zipcode: "",
    }
  },
  methods: {
    async getProductsData(zipcode) {
      const result = await fetch('https://zipcloud.ibsnet.co.jp/api/search?zipcode='+zipcode)
      .then(response => response.json())
      .catch(error => console.error(error));
      this.apiResult = JSON.stringify(result);
    },
  },
  async asyncData ({ $axios, params }) {
    const { data } = await $axios.get('https://jamstack--demo.microcms.io/api/v1/photo', {
      headers: { 'X-MICROCMS-API-KEY': process.env.MICROCMS_API_KEY }
    })
    return {
      items: data.contents
    }
  },
 }
 </script>
 <style module>
dialog {
  width:500px;
  padding: 0;
  border: 0;
  border-radius: 0.6rem;
  box-shadow: 0 0 1em black;
  z-index: 10;
  overflow-wrap: break-word;
  position: fixed;
}
 
dialog::backdrop {
  background-color: rgba(0, 0, 0, 0.4);
}
 </style>
