<template>
  <div>
    <h1>Latest Posts</h1>
    <div>
      <div v-for="article of articles" :key="article.slug">
        <nuxt-link :to="{ name: 'posts-slug', params: { slug: article.slug } }">
          <div
            class="mb-3 mx-auto sm:p-4 sm:grid grid-cols-5 bg-white shadow p-7 lg:max-w-2xl rounded-lg lg:col-span-2"
          >
            <img
              src="https://images.unsplash.com/photo-1502977249166-824b3a8a4d6d?ixid=MXwxMjA3fDB8MHxzZWFyY2h8MTd8fGZsb3dlcnxlbnwwfHwwfA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
              alt="Just a flower"
              class="w-full rounded-lg"
            />
            <div class="pt-5 self-center sm:pt-0 sm:pl-10 col-span-3">
              <h2 class="text-gray-800 capitalize text-xl font-bold">
                {{ article.title }}
              </h2>
              <p class="capitalize inline-block pt-2">
                {{ article.description }}
              </p>
            </div>
            <div class="justify-self-end">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                width="20px"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M14 10h4.764a2 2 0 011.789 2.894l-3.5 7A2 2 0 0115.263 21h-4.017c-.163 0-.326-.02-.485-.06L7 20m7-10V5a2 2 0 00-2-2h-.095c-.5 0-.905.405-.905.905 0 .714-.211 1.412-.608 2.006L7 11v9m7-10h-2M7 20H5a2 2 0 01-2-2v-6a2 2 0 012-2h2.5"
                />
              </svg>
            </div>
          </div>
          <!-- 
          <div
            class="mx-auto max-w-lg shadow-lg rounded overflow-hidden m-4 sm:flex"
          >
            <div
              class="h-48 sm:h-auto sm:w-48 md:w-64 flex-none bg-cover bg-center rounded rounded-t sm:rounded sm:rounded-l text-center overflow-hidden"
              style="background-image: url('https://unsplash.it/804/800')"
            ></div>

            <div class="px-6 py-4">
              <h2 class="mb-2 font-black"></h2>
              <p>
                {{ article.description }}
              </p>
            </div>
          </div> -->
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const articles = await $content("posts", params.slug)
      .only(["title", "description", "img", "slug"])
      .sortBy("createdAt", "asc")
      .fetch();

    return { articles };
  },
};
</script>

<style>
</style>