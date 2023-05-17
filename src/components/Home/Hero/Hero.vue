<script setup>
import { ref } from 'vue'
let obj = ref([])
let post = ref({})
let title = '';
let body = '';
let id  = '';
let api = 'https://jsonplaceholder.typicode.com/users/'
function getAll(){
    fetch(api)
    .then((res) => res.json())
    .then((data) => {
        obj.value = data
    })
}
function byId(e){
    const id = e.target.id
    posts(id)
}
function posts(id){
    fetch(api + id)
    .then((res) => res.json())
    .then((data) => post.value = data)
}
function POST() {
    fetch('https://jsonplaceholder.typicode.com/posts',{
        headers: {'Content-Type' : 'application/json'},
        method: 'POST',
        body: JSON.stringify({
            title: 'title' ,
            body: 'body'
        })
    }).then(res => res.json())
    .then(data => console.log(data))
}
function PUT() {
    let api = 'https://jsonplaceholder.typicode.com/users/'
    fetch( api + id,{
        headers: {'Content-Type' : 'application/json'},
        method: 'PUT',
        body: JSON.stringify({
            name: title,
            username: body
        })
    }).then(res => res.json())
    .then(data => console.log(data))
}
async function DELETE() {
    let api = 'https://jsonplaceholder.typicode.com/users/'
    let salom = await fetch( api + id,{
        headers: {'Content-Type' : 'application/json'},
        method: 'DELETE'
    })
    console.log(salom)
}
getAll()
</script>
<template>
    <section class="hero">
        <div class="container">
            <div class="hero__wrapper">
                <ul class="hero__list">
                    <li class="hero__item" v-for="item in obj" :key="item.id" :id="item.id" @click="byId">
                        {{ item.name }}
                    </li>
                </ul>
                <div class="card">
                    <div class="card__wrapper">
                        <h1 class="card__title">{{ post?.name }}</h1>
                        <h2 class="card__discription">{{ post?.username }}</h2>
                        <p class="card__text">{{ post?.email }}</p>
                    </div>
                </div>
                <div class="post">
                    <input type="text" v-model="title">
                    <input type="password" v-model="body">
                    <button @click="POST" >POST</button>
                </div>
                <div class="put">
                    <input type="text" v-model="title">
                    <input type="text" v-model="body">
                    <button @click="PUT">PUT</button>
                    <input type="number" v-model="id">
                </div>
                <div class="delete">
                    <input type="text" v-model="title">
                    <input type="text" v-model="body">
                    <button @click="DELETE">DELETE</button>
                    <input type="number" v-model="id">
                </div>
            </div>
        </div>
    </section>
    
</template>