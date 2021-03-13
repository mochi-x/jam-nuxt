<template>
  <div class="p-10">
    <ul class="grid grid-cols-3 gap-4">
      <li v-for="content in contents" :key="content.id">
        <nuxt-link class="text-center p-10 block w-full h-full" :to="`/${content.id}`">
          {{ content.title }}
        </nuxt-link>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  async asyncData({ $config, error }) {
    try {
      const { data } = await axios.get(
        'https://jam-nuxt.microcms.io/api/v1/blog',
        { headers: { 'X-API-KEY': $config.apiKey } }
      )
      return data
    } catch (err) {
      error({
        statusCode: err.response.status,
        message: err.response.data.message,
      });
    }
  }
}
</script>