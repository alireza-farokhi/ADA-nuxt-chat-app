<template>
  <div action="" class="box is-info">
    <div class="columns" :style="{ width: '100%', height: '2em' }">
      <div class="column">Chat</div>
    </div>

    <div
      v-for="(item, index) in messages"
      :key="index"
      :style="{
        padding: '.25em',
        justifyContent: 'flex-start',
        overflowWrap: 'normal',
        display: 'flex',
      }"
    >
      <div
        :style="{
          backgroundColor: item.role ? 'blue' : '#48c774',
          color: '#fff',
          padding: '.5em',
          wordWrap: 'break-word',
        }"
        :class="{
          'is-medium': true,
          'is-success': item.role ? false : true,
          'is-info': item.role ? true : false,
        }"
      >
        <label for="" class="label" :style="{ marginBottom: 0 }">{{
          item.username
        }}</label>

        <div>{{ item.message }}</div>
      </div>
    </div>
    <div class="field column is-12-desktop has-addons">
      <div class="control is-expanded">
        <input
          class="input"
          v-model="inputMessageOne"
          type="text"
          @keyup.enter="sendMessageOne(inputMessageOne)"
          placeholder="One:type message"
        />
      </div>
      <div class="control">
        <a class="button is-info" @click="sendMessageOne(inputMessageOne)"> Send</a>
      </div>

    </div>
    <div class="field column is-12-desktop has-addons">
      <div class="control is-expanded">
        <input
          class="input"
          v-model="inputMessageTwo"
          type="text"
          @keyup.enter="sendMessageTwo(inputMessageTwo)"
          placeholder="Two:type message"
        />
      </div>
      <div class="control">
        <a class="button is-info" @click="sendMessageTwo(inputMessageTwo)"> Send</a>
      </div>

    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Emit, Vue } from 'nuxt-property-decorator'
@Component
export default class Message extends Vue {
  inputMessageOne: string = ''
  inputMessageTwo: string = ''
  @Prop({ required: true }) readonly messages!: Array<object>
  @Emit()
  sendMessageOne(message: object): void {
    this.inputMessageOne = ''
  }
  @Emit()
  sendMessageTwo(message: object): void {
    this.inputMessageTwo = ''
  }
}
</script>
