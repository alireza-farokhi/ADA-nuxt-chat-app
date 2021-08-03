<template>
  <section class="hero is-primary is-fullheight">
    <div class="hero-body">
      <div class="container">
        <div class="columns is-centered">
          <div class="column is-12-tablet is-12-desktop is-12-widescreen">
            <Message
              :messages="messages"
              @send-message-one="sendOne"
              @send-message-two="sendTwo"
            />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script lang="ts">
import Message from '@/components/chat-component/Message.vue'
import { Component, Prop, Vue } from 'nuxt-property-decorator'

@Component({
  components: {
    Message,
  },
})
export default class Chat extends Vue {
  public connection: any
  public messages: Array<object> = []
  created() {
    this.connect()
  }

  connect() {
    console.log('Starting connection to WebSocket Server')
    this.connection = new WebSocket('wss://echo.websocket.org')
    console.log(this.connection)

    let ini = this
    this.connection.onmessage = function (event) {
      let data = JSON.parse(event.data)
      ini.messages.push(data)
    }

    this.connection.onopen = function (event) {
      console.log('Successfully connected to the echo websocket server...')
    }

    this.connection.onclose = function (event) {
      ini.messages = []
      console.log('Successfully closed connection the echo websocket server...')
    }
  }

  close() {
    if (1 === this.connection.readyState) {
      this.connection.close()
      this.connection = null
    }
  }
  sendOne(message: string): void {
    if (1 === this.connection.readyState)
      this.connection.send(
        JSON.stringify({ username: 'one', message: message })
      )
    if (message === 'restart') {
      this.close()
      this.connect()
    }
  }
  sendTwo(message: string): void {
    if (1 === this.connection.readyState)
      this.connection.send(
        JSON.stringify({ username: 'Two', message: message })
      )
    if (message === 'restart') {
      this.close()
      this.connect()
    }
  }
}
</script>
