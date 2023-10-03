<template>
    <div>
        <div v-for="postItem in posts" :key="postItem.id">
            <h2>{{ postItem.name }}</h2>
            <p>{{ postItem.usreName }}</p>
        </div>
    </div>
</template>
  

<script setup>
const route = useRoute();
const posts = ref([]);


const { data } = await useAsyncData('posts', async () => {
    const { data } = await client.from('posts').select();
    posts.value = data;
});

const post = computed(() => {
    return post.value.find((post) => post.id === route.params.id)
})

console.log(post);
</script>