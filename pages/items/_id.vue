<template>
  <div>
    <el-row type="flex" :data="item">
      <el-col :span="3">名称</el-col>
      <el-col :span="10">説明</el-col>
      <el-col :span="5">画像</el-col>
    </el-row>
    <hr />
    <el-row type="flex" :data="item">
      <el-col :span="3">{{item.name}}</el-col>
      <el-col :span="10">{{item.explain}}</el-col>
      <el-col :span="5"><img :src="item.image.url" /></el-col>
    </el-row>
  </div>
</template>
<script>
 export default {
  async asyncData ({ $axios, params }) {
    const { data } = await $axios.get('https://jamstack--demo.microcms.io/api/v1/photo/'+params.id, {
      headers: { 'X-MICROCMS-API-KEY': 'd5a89b117ef64b58bc511f4089e8b0c84aca' }
    })
    return {
      item: data
    }
  },
 }
 </script>
