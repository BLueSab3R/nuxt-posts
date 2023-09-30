<template>
  <ul role="list ">
    <li class="col-span-1 divide-y divide-gray-200 rounded-lg bg-white shadow mb-2 mt-2">
      <div class="flex w-full items-center justify-between space-x-6 p-6">
        <div class="flex-1 truncate">
          <div class="text-xl">username: {{ user.username }}</div>
          <div class="text-xm">website:{{ user.website }}</div>
          <div class="text-xm">email: {{ user.email }}</div>
        </div>
      </div>
      <div>
        <div class="-mt-px flex divide-x divide-gray-200">
          <div class="flex w-0 flex-1 hover:bg-sky-400">
            <button
              @click="editHandle(user)"
              class="relative -mr-px inline-flex w-0 flex-1 items-center justify-center gap-x-3 rounded-bl-lg border border-transparent py-4 text-sm font-semibold text-gray-900"
            >
              Edit
            </button>
          </div>
          <div class="-ml-px flex w-0 flex-1 hover:bg-red-400">
            <button
              @click="deleteHandle(user)"
              class="relative inline-flex w-0 flex-1 items-center justify-center gap-x-3 rounded-br-lg border border-transparent py-4 text-sm font-semibold text-gray-900"
            >
              Delete
            </button>
          </div>
        </div>
      </div>
    </li>
  </ul>
</template>

<script setup>
const { user } = defineProps(['user']);
const emit = defineEmits(['openEdit', 'openDelete']);
const editHandle = (user) => {
  emit('openEdit', user);
};
const deleteHandle = (user) => {
  emit('openDelete', user);
};
</script>
