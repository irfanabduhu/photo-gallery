<script setup>
import { ref, onMounted } from 'vue';
import Gallery from './Gallery.vue';

const keyword = ref("")
const author = ref("")
const year = ref("")
const searchResults = ref([])

async function search() {
    const res = await fetch('/data.json')
    const data = await res.json();
    let filteredData = data;

    searchResults.value = null;

    if (author.value) {
        console.log("AUTHOR", author.value);
        filteredData = filteredData.filter(item => item.author === author.value)
    }
    if (year.value) {
        console.log("YEAR", year.value);
        filteredData = filteredData.filter(item => item.year === +year.value)
    }
    if (keyword.value.trim()) {
        const searchTerm = keyword.value.trim();
        console.log("SEARCH", searchTerm)
        filteredData = filteredData.filter(item => {
            return (item.title.includes(searchTerm)
                || item.author.includes(searchTerm)
                || searchTerm.includes(item.year)
                || item.description.includes(searchTerm))
        })
    }

    setTimeout(() => {
        searchResults.value = filteredData
    }, 1000)
}

onMounted(search);
</script>

<template>
    <div class="w-2/3 mx-auto">
        <div class="flex flex-col w-2/3 mt-6 mb-4 ">
            <h1 class="text-3xl font-bold">Search</h1>
            <div class="flex flex-row justify-between my-4">
                <input type="text" placeholder="Search"
                    class="w-1/3 px-4 py-2 bg-gray-100 border rounded-md focus:bg-white" v-model="keyword"
                    @blur="search">
                <select name="author" class="w-1/4 px-4 py-2 bg-gray-100 border rounded-md focus:bg-white"
                    v-model="author" @change="search">
                    <option value="">Author</option>
                    <option value="Irfanul Hoque">Irfanul Hoque</option>
                    <option value="Hasan">Hasan</option>
                    <option value="Rafi">Rafi</option>
                </select>
                <select name="year" class="w-1/4 px-4 py-2 bg-gray-100 rounded-md focus:bg-white" v-model="year"
                    @change="search">
                    <option value="">Year</option>
                    <option value="2020">2020</option>
                    <option value="2021">2021</option>
                    <option value="2022">2022</option>
                </select>
            </div>
        </div>
    </div>
    <Gallery :photoList="searchResults" />
</template>