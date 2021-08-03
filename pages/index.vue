<template>
  <Chat />
</template>

<script lang="ts">
import Chat from '@/components/chat-component/Chat.vue'
import { Component, Vue } from 'nuxt-property-decorator'
@Component({
  components: {
    Chat
  }
})
export default class MyStore extends Vue {

}
</script>
