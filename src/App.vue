<template>
  <div class="header">
    <ul class="header-button-left">
      <li>Cancel</li>
    </ul>
    <ul class="header-button-right">
      <li v-if="step == 1" @click="step++;">Next</li>
      <li v-if="step == 2" @click="publish">Next</li>
    </ul>
    <img src="./assets/logo.png" class="logo" />
  </div>

  <Container :data = "data" :step= "step" :url = "url"/>
  <button @click="more">더보기</button>
  
  <div class="footer">
    <ul class="footer-button-plus">
      <input @change="upload" type="file" id="file" class="inputfile" />
      <label for="file" class="input-plus">+</label>
    </ul>
  </div>
  
  <button @click="step = 0">전체보기</button>
  <button @click="step = 1">상세보기</button>
  <button @click="step = 2">등록하기</button>
</template>

<script>
  import Container from './components/Container';
  import data from './assets/data.js';
  import axios from 'axios';


export default {
  name: 'App',
  components: {
    Container,
  },
  data(){
    return {
      step : 0,
      data : data,
      url : '',
      작성한글 : '',
    }
  },
  methods:{
    publish(){
      var 내게시물 = {
      name: "Kim Hyun",
      userImage: "https://placeimg.com/100/100/arch",
      postImage: this.url,
      likes: 36,
      date: "May 15",
      liked: false,
      content: this.작성한글,
      filter: "perpetua"
    };
      this.data.unshift(내게시물);
      this.step = 0;
    },
    more(){
      //axios.post('URL' , {name : 'kim'}).then().catch((err)=> {});
      axios.get('https://codingapple1.github.io/vue/more0.json')
      .then((data) => {
        console.log(data.data);
        this.data.push(data.data);      
      })
    },
    upload(e){
      let a = e.target.files;
      console.log(e);
      let url = URL.createObjectURL(a[0]);
      this.url = url;
      this.step++;
    }

  }
}
</script>

<style>
    body {
    margin: 0;
  }
  ul {
    padding: 5px;
    list-style-type: none;
  }
  .logo {
    width: 22px;
    margin: auto;
    display: block;
    position: absolute;
    left: 0;
    right: 0;
    top: 13px;
  }
  .header {
    width: 100%;
    height: 40px;
    background-color: white;
    padding-bottom: 8px;
    position: sticky;
    top: 0;
  }
  .header-button-left {
    color: skyblue;
    float: left;
    width: 50px;
    padding-left: 20px;
    cursor: pointer;
    margin-top: 10px;
  }
  .header-button-right {
    color: skyblue;
    float: right;
    width: 50px;
    cursor: pointer;
    margin-top: 10px;
  }
  .footer {
    width: 100%;
    position: sticky;
    bottom: 0;
    padding-bottom: 10px;
    background-color: white;
  }
  .footer-button-plus {
    width: 80px;
    margin: auto;
    text-align: center;
    cursor: pointer;
    font-size: 24px;
    padding-top: 12px;
  }
  .sample-box {
    width: 100%;
    height: 600px;
    background-color: bisque;
  }
  .inputfile {
    display: none;
  }
  .input-plus {
    cursor: pointer;
  }
  #app {
    box-sizing: border-box;
    font-family: "consolas";
    margin-top: 60px;
    width: 100%;
    max-width: 460px;
    margin: auto;
    position: relative;
    border-right: 1px solid #eee;
    border-left: 1px solid #eee;
  }
</style>
