<template>
  <div>
    <h1>Latest Posts</h1>
    <div>
      <div v-for="article of articles" :key="article.slug">
        <nuxt-link :to="{ name: 'posts-slug', params: { slug: article.slug } }">
          <div class="mx-auto max-w-lg shadow-lg rounded overflow-hidden m-4 sm:flex">
            <div
              class="h-48 sm:h-auto sm:w-48 md:w-64 flex-none bg-cover bg-center rounded rounded-t sm:rounded sm:rounded-l text-center overflow-hidden"
              style="background-image: url('https://unsplash.it/804/800')"
            ></div>

            <div class="px-6 py-4">
              <h2 class="mb-2 font-black">{{ article.title }}</h2>
              <p>
                {{ article.description }}
              </p>
            </div>
          </div>
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