<template>
  <div class="container">
    <div class="section">
      <div class="field">
        <textarea v-model="input" spellcheck="false" class="textarea" :class="{ 'is-danger': error.length > 0}" placeholder="Paste study data here" />
        <p v-show="error.length > 0" class="help is-danger">
          {{ error }}
        </p>
      </div>
      <div class="field">
        <button class="button is-primary is-fullwidth" @click="convert">
          Convert
        </button>
      </div>
    </div>
    <div class="section">
      <Speech v-for="speechEvent in speechEvents" :key="speechEvent.key" />
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      input: '',
      error: '',
      speechEvents: []
    }
  },

  methods: {
    convert () {
      try {
        this.speechEvents = []
        this.error = ''

        const result = JSON.parse(this.input)

        result.forEach((event, index) => {
          if (index < result.length - 1) {
            const seconds = (result[index + 1].timestamp - event.timestamp) / 1000

            this.speechEvents.push({
              speakerName: event.speakerName,
              speechDuration: seconds,
              key: Math.floor(Math.random() * Date.now())
            })
          }
        })
      } catch (e) {
        this.error = e.toString()
      }
    }
  }
}
</script>
