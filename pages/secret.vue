<template>
  <div>
    <h1>Message from Server.</h1>
    {{reply}}
    <NuxtLink to="/">
      Back home
    </NuxtLink>
  </div>
</template>

<script>
import axios from 'axios'
// const cookieparser = process.server ? require('cookieparser') : undefined
import Cookies from 'js-cookie'
export default {
  middleware: 'authenticated',
  async asyncData( {params} ) {
      const { data } = await axios.post(
            `http://127.0.0.1:5000/talk`,
            {sentence:'hi,woshi liuquanfeng'},
            {
                headers: {'Authorization': Cookies.get('auth')},
            }
        )
    return { reply: data }
  },
}
</script>
