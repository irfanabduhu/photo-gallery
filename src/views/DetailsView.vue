<script setup>
import { onMounted, reactive, ref } from 'vue';
import { useRouter } from 'vue-router'
import MapViewer from '../components/MapViewer.vue'

const { currentRoute } = useRouter();
const id = +currentRoute.value.params.id;

const story = reactive({
    details: null
});

const position = reactive({
    latlong: []
})


async function fetchById() {
    const res = await fetch('/data.json')
    const json = await res.json();
    const item = json.find(t => t.id === id);
    story.details = item;
    position.latlong = story.details.position;
}

onMounted(fetchById);
</script>

<template>
    <div class="flex flex-row w-4/5 mx-auto my-4 bg-red-100">
        <MapViewer :latlong="position.latlong" />
        <div class="flex flex-col w-1/2 bg-blue-100">
            <div v-if="story.details">
                <img :src="story.details.imageUrl" alt="" />
                <div class="px-4 py-10">
                    <h1 class="text-6xl font-bold capitalize text-slate-900">
                        {{ story.details.title }}
                    </h1>
                    <h2 class="text-2xl">
                        By <span class="font-bold"> {{ story.details.author }} </span>
                    </h2>
                    <h3 class="mb-4 text-xl text-slate-700">
                        Published in
                        <span class="font-bold">{{ story.details.year }}</span>
                    </h3>
                    <p class="text-lg text-justify">
                        {{ story.details.description }}
                    </p>
                </div>
            </div>
            <div v-else>
                <h1>Loading...</h1>
            </div>
        </div>
    </div>
</template>