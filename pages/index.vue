<template>
  <div>
    <div>
      <h1>写真一覧</h1>
      <el-table
        :data="items">
        <el-table-column>
          <template slot-scope="scope">
           <nuxt-link :to="'/items/'+scope.row.id"><img :src="scope.row.image.url" /></nuxt-link>
          </template>
        </el-table-column>
      </el-table>
    </div>
  </div>
</template>
<script>
 export default {
  data () {
    return {
      items: []
    }
  },
  async asyncData ({ $axios, params }) {
    const { data } = await $axios.get('https://jamstack--demo.microcms.io/api/v1/photo', {
      headers: { 'X-MICROCMS-API-KEY': 'd5a89b117ef64b58bc511f4089e8b0c84aca' }
    })
    return {
      items: data.contents
    }
  },
 }
 </script>
