<template>
  <div
    @click="handleBackgroundClick"
    class="fixed flex flex-col items-center justify-center max-h-screen inset-0 overflow-y-auto bg-black bg-opacity-50"
  >
    <div class="bg-white flex flex-col text-black w-1/2 rounded-lg relative">
      <h3 class="flex justify-center text-xl">Add new post</h3>
      <button
        @click="$emit('closeAdd')"
        class="absolute top-2 right-2 rounded-md border-red-400 bg-red-400 border-solid text-xl hover:bg-red-200 border-2"
      >
        Close
      </button>

      <ul class="text-xl">
        <li>
          <label class="mr-2" for="username">Username:</label>
          <input
            id="username"
            name="username"
            v-model="formData.username"
            type="text"
            placeholder="new username"
          />
        </li>
        <li>
          <label class="mr-2" for="name">Name:</label>
          <input
            id="name"
            name="name"
            v-model="formData.name"
            type="text"
            placeholder="new name"
          />
        </li>
        <li>
          <label class="mr-2" for="email">Email:</label>
          <input
            id="email"
            name="email"
            v-model="formData.email"
            type="text"
            placeholder="new email"
          />
        </li>
        <li>
          <label class="mr-2" for="website">Website:</label>
          <input
            id="website"
            name="website"
            v-model="formData.website"
            type="text"
            placeholder="new website"
          />
        </li>
        <li>
          <label class="mr-2" for="city">City:</label>
          <input
            id="city"
            name="city"
            v-model="formData.city"
            type="text"
            placeholder="new city"
          />
        </li>
        <li>
          <label class="mr-2" for="phone">Phone:</label>
          <input
            id="phone"
            name="phone"
            v-model="formData.phone"
            type="text"
            placeholder="new phone"
          />
        </li>
        <li>
          <label class="mr-2" for="street">Street:</label>
          <input
            id="street"
            name="street"
            v-model="formData.street"
            type="text"
            placeholder="new street"
          />
        </li>
        <li>
          <label class="mr-2" for="suite">Suite:</label>
          <input
            id="suite"
            name="suite"
            v-model="formData.suite"
            type="text"
            placeholder="new suite"
          />
        </li>
        <li>
          <label class="mr-2" for="zipcode">Zipcode:</label>
          <input
            id="zipcode"
            name="zipcode"
            v-model="formData.zipcode"
            type="text"
            placeholder="new Zipcode"
          />
        </li>
        <li>
          <label class="mr-2" for="company_name">Company name:</label>
          <input
            id="company_name"
            name="company_name"
            v-model="formData.company_name"
            type="text"
            placeholder="new Company name"
          />
        </li>
        <li>
          <label class="mr-2" for="bs">Bs:</label>
          <input
            id="bs"
            name="bs"
            v-model="formData.bs"
            type="text"
            placeholder="new bs"
          />
        </li>
        <li>
          <label class="mr-2" for="catchPhrase">Catch phrase:</label>
          <input
            id="catchPhrase"
            name="catchPhrase"
            v-model="formData.catchPhrase"
            type="text"
            placeholder="new catch phrase"
          />
        </li>
      </ul>
      <button @click="confirmAdd" class="mt-20">Confirm</button>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient();
const emit = defineEmits(["closeAdd", "updatePosts"]);
const formData = ref({
  username: "",
  name: "",
  email: "",
  website: "",
  city: "",
  phone: "",
  street: "",
  suite: "",
  zipcode: "",
  company_name: "",
  bs: "",
  catchPhrase: "",
});
const confirmAdd = async () => {
  const { error } = await supabase.from("posts").insert([formData.value]).select();
  if (!error) {
    emit("closeAdd");
    emit("updatePosts");
  } else {
    console.log(error);
  }
};
const handleBackgroundClick = (event) => {
  if (event.target === event.currentTarget) {
    emit("closeAdd");
  }
};
</script>
