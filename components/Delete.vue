<template>
  <div
    @click="handleBackgroundClick"
    class="fixed flex items-center justify-center max-h-screen inset-0 overflow-y-auto bg-black bg-opacity-50"
  >
    <div class="bg-white text-black rounded-lg p-40 relative">
      <button
        @click="$emit('closeDelete')"
        class="absolute top-2 right-2 rounded-md border-red-400 bg-red-400 border-solid text-xl hover:bg-red-200 border-2"
      >
        Close
      </button>
      <h2>Are you sure you want to delete?</h2>
      <button
        class="absolute bottom-2 border-none text-xl hover:bg-red-200 border-2"
        @click="deletePost"
      >
        Confirm
      </button>
    </div>
  </div>
</template>

<script setup>
const client = useSupabaseClient();
const emit = defineEmits(['closeDelete', 'updatedFetch']);
const props = defineProps(['selectedPost']);

const deletePost = async () => {
  const { error } = await client.from('posts').delete().eq('id', props.selectedPost.id);
  if (!error) {
    emit('closeDelete');
    location.reload();
  }
};
</script>
