<template>
  <div class="container">
    <h1>非同期通信</h1>
    <p>JSONPlaceholder によるダミー・ユーザーデータの取得 <br> axiosを使用</p>
    <div class="field-b">
      <h2>v-forでループ処理</h2>
      <ul>
        <li v-for="user in users" v-bind:key="user.id">{{ user.id}} : {{ user.name}} | company : {{ user.company.name }} </li>
      </ul>
    </div>
    <hr>
    <h2>画像の表示</h2>
    <img src="~/assets/spa.png" alt="">
  </div>
</template>

<script>
// import Logo from '~/components/Logo.vue'
  const axios = require('axios') // axiosのインスタンスを生成（使えるようにする）
  let url = 'https://jsonplaceholder.typicode.com/users'

export default {
  asyncData({params, error}){ // asyncDataメソッド→Nuxtで用意されている、componentを初期化する前に非同期の処理を行う為のメソッド
      return axios.get(url) // apiからのデータ取得をリクエスト
      .then((res) => { // resにはサーバーから受け取ったレスポンスデータが入っている
        return { users: res.data } // res.data には送られてきたjsonが。尚、レスポンスデータは、axiosによってjsのオブジェクトに変換されている。
      }) // res.dataに users という名前をつけて、テンプレート側でマスタッシュ構文で呼び出す
      .catch((e => { //eにエラーデータ
        // console.log(e.response.status)
        // error({ users: e.response.status, message: e.message }) // errorメソッド→エラーページを表示するためのもの
        error({ users: e.response.status, message: '不測の事態なう' }) // errorメソッド→エラーページを表示するためのもの
      }))
  }
}
</script>

<style>
.container {
  /* margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center; */
}
h1{
  margin: 40px 0 10px 10px;
}
p{
  margin: 20px 0 40px 20px;
  color: #333;
}
.field-a,
.field-b{
  margin: 20px;
}
ul{
  /* width: fit-content; */
  padding: 10px;
  list-style:none;
  display: flex;
  flex-direction: column;
    border: solid gray 1px
}
li{
  width: fit-content;
  padding: 10px;
  /* border: solid gray 1px */
}
img{
  width: 50vw;
}
</style>
