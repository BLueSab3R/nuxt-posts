<template>
  <div @click="handleBackgroundClick"
    class="fixed flex flex-col items-center justify-center max-h-screen inset-0 overflow-y-auto bg-black bg-opacity-50">
    <div class="bg-white flex flex-col text-black p-40 rounded-lg relative">

      <button @click="$emit('closeEdit')"
        class="absolute top-2 right-2 rounded-md border-red-400 bg-red-400 border-solid text-xl hover:bg-red-200 border-2">
        Close
      </button>

      <ul class="text-xl">
        <li>
          <label class="mr-2">Username:</label>
          <input type="text" v-model="selectedPost.username" placeholder="new username" />
        </li>
        <li>
          <label class="mr-2">Name:</label>
          <input type="text" v-model="selectedPost.name" placeholder="new name" />
        </li>
        <li>
          <label class="mr-2">Email:</label>
          <input type="text" v-model="selectedPost.email" placeholder="new email" />
        </li>
        <li>
          <label class="mr-2">Website:</label>
          <input type="text" v-model="selectedPost.website" placeholder="new website" />
        </li>
        <li>
          <label class="mr-2">City:</label>
          <input type="text" v-model="selectedPost.city" placeholder="new city" />
        </li>
        <li>
          <label class="mr-2">Phone:</label>
          <input type="text" v-model="selectedPost.phone" placeholder="new phone" />
        </li>
      </ul>
      <button class="flex mt-20 justify-center" @click="updatePost">Confirm</button>
    </div>
  </div>
</template>

<script setup>
const client = useSupabaseClient();
const emit = defineEmits(['closeEdit', 'updatePosts']);
const props = defineProps(['selectedPost']);
const handleBackgroundClick = (event) => {
  if (event.target === event.currentTarget) {
    emit('closeEdit');
  }
};

const updatePost = async () => {
  const updatedData = {
    username: props.selectedPost.username || null,
    name: props.selectedPost.name || null,
    email: props.selectedPost.email || null,
    city: props.selectedPost.city || null,
  };
  const { data, error } = await client
    .from('posts')
    .update(updatedData)
    .eq('id', props.selectedPost.id);
  if (!error) {
    emit('updatePosts', 'closeEdit');
  } else {
    console.error(error);
  }
};
</script>
