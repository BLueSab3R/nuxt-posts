<template>
  <div @click="handleBackgroundClick"
    class="fixed flex flex-col items-center justify-center max-h-screen inset-0 overflow-y-auto bg-black bg-opacity-50">
    <div class="bg-white flex flex-col text-black w-1/2	 rounded-lg relative">
      <h3 class="flex justify-center text-xl">Add new post</h3>
      <button @click="$emit('closeAdd')"
        class="absolute top-2 right-2 rounded-md border-red-400 bg-red-400 border-solid text-xl hover:bg-red-200 border-2">
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
        <li>
          <label class="mr-2">Street:</label>
          <input v-model="formData.street" type="text" placeholder="new street" />
        </li>
        <li>
          <label class="mr-2">Suite:</label>
          <input v-model="formData.suite" type="text" placeholder="new suite" />
        </li>
        <li>
          <label class="mr-2">Zipcode:</label>
          <input v-model="formData.zipcode" type="text" placeholder="new Zipcode" />
        </li>
        <li>
          <label class="mr-2">Company name:</label>
          <input v-model="formData.company_name" type="text" placeholder="new Company name" />
        </li>
        <li>
          <label class="mr-2">Bs:</label>
          <input v-model="formData.bs" type="text" placeholder="new bs" />
        </li>
        <li>
          <label class="mr-2">Catch phrase:</label>
          <input v-model="formData.catchPhrase" type="text" placeholder="new catch phrase" />
        </li>
      </ul>
      <button @click="confirmAdd" class="mt-20">Confirm</button>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient();
const emit = defineEmits(['closeAdd', 'updatePosts']);
const formData = ref({
  username: '',
  name: '',
  email: '',
  website: '',
  city: '',
  phone: '',
  street: '',
  suite: '',
  zipcode: '',
  company_name: '',
  bs: '',
  catchPhrase: '',
});
const confirmAdd = async () => {
  const { data, error } = await supabase
    .from('posts')
    .insert([formData.value])
    .select();
  if (!error) {
    emit('closeAdd')
    emit('updatePosts');
  } else {
    console.log(error);
  }
};
const handleBackgroundClick = (event) => {
  if (event.target === event.currentTarget) {
    emit('closeAdd');
  }
};
</script>
