<template>
  <section>
    <h1>Qiita 新着記事一覧</h1>
    <div v-for="(article, index) in articleList" :key="index">
      <ul class="list-group">
        <li class="list-group-item">
          <a :href="article.url">{{ article.title }}</a>
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
// axios
import axios from 'axios'
// qiita api URL
const BASE_URL = 'https://qiita.com/api/v2/'

export default {
  async asyncData(context) {
    try {
      const response = await axios.get(BASE_URL + 'items', {
        params: {
          page: 1,
          per_page: 10,
        },
      })
      return {
        articleList: response.data,
      }
    } catch (error) {
      console.log(error)
    }
  },
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  border-top: 5px solid rgb(0, 199, 0);
  padding: 0 0 100px 0;
  background: #efefef;
}
a {
  color: crimson;
}
ul li {
  list-style: none;
}
h1 {
  text-align: center;
  font-size: 35px;
  line-height: 1.25em;
  margin: 0 0 50px 0;
  padding: 0 0 5px 0;
  transform: rotate(-5deg);
  color: rgb(0, 199, 0);
  border-bottom: 2px solid rgb(0, 199, 0);
  right: 70px;
  position: relative;
}
h2 {
  font-size: 20px;
  font-weight: 500;
}
.container {
  width: 60%;
  margin: 50px auto;
}
.item-lists {
  margin: 15px 0 0 0;
}
.item-lists .item-list {
  padding: 25px 30px 15px;
  border-bottom: 1px solid #ccc;
  background: #fff;
}
.item-lists .item-list:last-child {
  border-bottom: none;
}
.item-lists .item-list h3 {
  font-size: 18px;
  font-weight: 500;
  line-height: 1.5em;
  letter-spacing: -0.25px;
  margin: 0 0 10px 0;
}
.item-lists .item-list h3 p {
  font-size: 12px;
  font-weight: 100;
}
.item-lists .item-list h4 {
  font-size: 15px;
  font-weight: 300;
  line-height: 1.75em;
  margin: 0 0 15px 0;
}

@media screen and (max-width: 768px) {
  body {
    padding: 0;
  }
  h1 {
    font-size: 25px;
    padding: 0 15px 15px;
    right: 0px;
    transform: rotate(0deg);
  }
  h2 {
    padding: 0 0 0 30px;
  }
  .container {
    width: 100%;
    margin: 50px auto 0;
  }
}
</style>
