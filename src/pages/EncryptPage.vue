<template>
  <q-page class="flex flex-center">
    <q-card dark bordered class="bg-grey-9 col q-ma-lg">
      <q-card-section>
        <div class="text-h6">Encrypt</div>
      </q-card-section>
      <q-separator dark inset />
      <q-card-section>
        <form @submit.prevent.stop="encryptPost" @reset.prevent.stop="onReset" class="q-gutter-md">
          <q-input required dark standout v-model="phrase" label="Phrase" class="q-mb-sm" :rules="[val => !!val || 'Phrase is required']"/>
          <q-input dark standout v-model="uuid" label="UUID" class="q-mb-lg"/>
          <div>
            <q-btn label="Submit" type="submit" color="primary" class="q-mr-md" />
            <span>{{this.sending ? "Sending..." : ""}}</span>
          </div>
        </form>
      </q-card-section>
      <div v-if="response && response.status == 200">
        <q-separator dark inset />
        <q-card-section>
          <div class="text-h6">Result</div>
          <div class="text-body overflow-auto q-pb-sm">{{response.data.encryptedPhrase}}</div>
        </q-card-section>
      </div>
      <div v-if="error">
        <q-separator dark inset />
        <q-card-section>
          <div>{{error}}</div>
        </q-card-section>
      </div>
    </q-card>
  </q-page>
</template>

<script>
export default {
  name: 'EncrpytPage',
  data () {
    return {
      sending: false,
      uuid: '',
      phrase: '',
      title: 'Encrypt',
      response: null,
      error: null
    }
  },
  methods: {
    async encryptPost () {
      let payload = {}
      payload.phrase = this.phrase
      if (this.uuid) {
        payload.uuid = this.uuid
      }
      try {
        this.sending = true
        this.response = await this.$axios.post(this.$apiurl + '/encrypt/', payload)
      } catch (error) {
        this.error = error
      } finally {
        this.sending = false
      }
    }
  }
}
</script>

<style>
  .q-field__messages {
    color: white;
  }
</style>
