<template>
  <div
    @click="handleBackgroundClick"
    class="fixed flex flex-col items-center justify-center max-h-screen inset-0 overflow-y-auto bg-black bg-opacity-50"
  >
    <div class="bg-white flex flex-col text-black w-300 rounded-lg relative">
      <h3 class="flex justify-center text-xl">Add new post</h3>
      <button
        @click="$emit('closeAdd')"
        class="absolute top-2 right-2 rounded-md border-red-400 bg-red-400 border-solid text-xl hover:bg-red-200 border-2"
      >
        Close
      </button>

      <ul class="text-xl">
        <li>
          <label class="mr-2">Username:</label>
          <input v-model="formData.username" type="text" placeholder="new username" />
        </li>
        <li>
          <label class="mr-2">Name:</label>
          <input v-model="formData.name" type="text" placeholder="new name" />
        </li>
        <li>
          <label class="mr-2">Email:</label>
          <input v-model="formData.email" type="text" placeholder="new email" />
        </li>
        <li>
          <label class="mr-2">Website:</label>
          <input v-model="formData.website" type="text" placeholder="new website" />
        </li>
        <li>
          <label class="mr-2">City:</label>
          <input v-model="formData.city" type="text" placeholder="new city" />
        </li>
        <li>
          <label class="mr-2">Phone:</label>
          <input v-model="formData.phone" type="text" placeholder="new phone" />
        </li>
      </ul>
      <button @click="confirmAdd" class="mt-20">Confirm</button>
    </div>
  </div>
</template>

<script setup>
const client = useSupabaseClient();
const emit = defineEmits(['closeAdd']);
const props = defineProps(['ids']);
const formData = ref({
  username: '',
  name: '',
  email: '',
  website: '',
  city: '',
  phone: '',
});
const handleBackgroundClick = (event) => {
  if (event.target === event.currentTarget) {
    emit('closeAdd');
  }
};
const generateUniqueId = () => {
  let newId = null;
  do {
    newId = Math.floor(Math.random() * 100);
  } while (props.ids.some((item) => item.id === newId));
  return newId;
};
const confirmAdd = async () => {
  const newId = generateUniqueId();
  formData.id = newId;
  const { data, error } = await client.from('posts').insert([formData.value]).select();
  if (!error) {
    emit('closeAdd');
    location.reload();
  } else {
    console.log(error);
  }
};
</script>
