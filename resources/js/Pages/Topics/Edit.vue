<template>
  <Head title="Topics" />

  <BreezeAuthenticatedLayout>
    <template #header>
      <h2 class="font-semibold text-xl text-gray-800 leading-tight">
        Topics Index
      </h2>
    </template>

    <div class="py-12">
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <div class="flex m-2 p-2">
          <Link
            href="/topics"
            class="
              px-4
              py-2
              bg-indigo-500
              hover:bg-indigo-600
              text-white
              rounded
            "
            >Back</Link
          >
        </div>
        <div class="">
          <div class="grid place-content-center mt-10">
            <form
              @submit.prevent="updateTopic"
              class="bg-white shadow-md m-2 p-2 rounded"
            >
              <div class="sm:col-span-6">
                <label
                  for="title"
                  class="block text-sm font-medium text-gray-700"
                >
                  Name
                </label>
                <div class="mt-1">
                  <input
                    type="text"
                    id="title"
                    name="title"
                    v-model="form.name"
                    class="
                      block
                      w-full
                      transition
                      duration-150
                      ease-in-out
                      appearance-none
                      bg-white
                      border border-gray-400
                      rounded-md
                      py-2
                      px-3
                      text-base
                      leading-normal
                      transition
                      duration-150
                      ease-in-out
                      sm:text-sm sm:leading-5
                    "
                  />
                </div>
              </div>
              <div class="sm:col-span-6">
                <label
                  for="title"
                  class="block text-sm font-medium text-gray-700"
                >
                  Image
                </label>
                <div class="m-2 p-2">
                  <img :src="image" class="w-32 h-32" />
                </div>
                <div class="mt-1">
                  <input
                    type="file"
                    id="image"
                    name="image"
                    @input="form.image = $event.target.files[0]"
                    class="
                      block
                      w-full
                      transition
                      duration-150
                      ease-in-out
                      appearance-none
                      bg-white
                      border border-gray-400
                      rounded-md
                      py-2
                      px-3
                      text-base
                      leading-normal
                      transition
                      duration-150
                      ease-in-out
                      sm:text-sm sm:leading-5
                    "
                  />
                </div>
              </div>
              <div class="m-2 p-2">
                <button
                  type="submit"
                  class="
                    px-4
                    py-2
                    bg-green-400
                    hover:bg-green-600
                    rounded-lg
                    text-white
                  "
                >
                  Update
                </button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </BreezeAuthenticatedLayout>
</template>

<script setup>
import BreezeAuthenticatedLayout from "@/Layouts/Authenticated.vue";
import { Head, Link, useForm } from "@inertiajs/inertia-vue3";
import { Inertia } from "@inertiajs/inertia";

const props = defineProps({
  topic: Object,
  image: String,
});

const form = useForm({
  name: props.topic.name,
  image: null,
});

function updateTopic() {
  Inertia.post(`/topics/${props.topic.id}`, {
    _method: "put",
    name: form.name,
    image: form.image,
  });
}
</script>
