<template>
  <section class="hero is-primary is-fullheight">
    <div class="hero-body">
      <div class="container">
        <div class="columns is-centered">
          <div class="column is-12-tablet is-12-desktop is-12-widescreen">
            <Message @logout="logout" :messages="messages" @send-message="send" />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script lang="ts">
import Message from '@/components/chat-component/Message.vue'
import { Component, Prop, Vue } from 'nuxt-property-decorator'
import Cookies from 'js-cookie'


@Component({
  components: {
    Message,
  },
})
export default class Chat extends Vue {
  public ws: any
  public messages: Array<object> = []
  public socket: any
  logout() {
    Cookies.remove('user')
    this.$router.push('/')
  }
  created() {

  }
  send(message: string): void {

  }
}
</script>
