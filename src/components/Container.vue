<template>
  <div>
    <div v-if="step == 0">
        <Post :data = "data[i]" v-for="(a,i) in data" :key="i"/>
    </div>
    <!-- 필터선택페이지 -->
    <div v-if="step == 1">
        <div class="upload-image" :style="`background-image:url(${url})`"></div>
        <div class="filters">
            <FilterBox :url="url" v-for="a in filterData" :key="a"></FilterBox>
        </div>
    </div>
    <!-- 글작성페이지 -->
    <div v-if="step == 2">
        <div class="upload-image" :style="`background-image:url(${url})`"></div>
        <div class="write">
            <textarea class="write-box" @input="$emit('write', $event.target.value)">write!</textarea>
        </div>
    </div>

</div>
</template>

<script>

import Post from './Post.vue'
import FilterBox from './FilterBox.vue'
import filterData from './assets/filterData.js';
export default {
    components : {
        Post, 
        FilterBox,
    },
    props : {
        data : Array,
        step : Number,
        url : String,
    },
    data(){
        return {
            filterData : filterData,
        }
    }
}
</script>

<style>
    .upload-image{
    width: 100%;
    height: 450px;
    background: cornflowerblue;
    background-size : cover;
    }
    .filters{
    overflow-x:scroll;
    white-space: nowrap;
    }
    .filter-1 {
    width: 100px;
    height: 100px;
    background-color: cornflowerblue;
    margin: 10px 10px 10px auto;
    padding: 8px;
    display: inli0-block;
    color : white;
    background-size: cover;
    }
    .filters::-webkit-scrollbar {
    height: 5px;
    }
    .filters::-webkit-scrollbar-track {
    background: #f1f1f1; 
    }
    .filters::-webkit-scrollbar-thumb {
    background: #888; 
    border-radius: 5px;
    }
    .filters::-webkit-scrollbar-thumb:hover {
    background: #555; 
    }
    .write-box {
    border: none;
    width: 90%;
    height: 100px;
    padding: 15px;
    margin: auto;
    display: block;
    outline: none;
    }
</style>