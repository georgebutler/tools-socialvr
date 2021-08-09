<template>
  <main>
    <div class="container">
      <div class="section">
        <h1 class="title">
          Social VR Study Data Tool
        </h1>
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
        <h2 class="subtitle">
          Speech Events
        </h2>
        <p v-if="speechEvents.length <= 0">
          Speech events will be listed here
        </p>
        <Speech v-for="speechEvent in speechEvents" :key="speechEvent.key" :speaker="speechEvent.speaker" :duration="speechEvent.duration" />
      </div>
    </div>
    <footer class="footer">
      <div class="content has-text-centered">
        <p>
          <strong>Social VR Study Data Tool</strong> by <a href="https://github.com/georgebutler">George Butler</a>.
        </p>
        <p>The source code is licensed <a href="http://opensource.org/licenses/mit-license.php">MIT</a>.</p>
      </div>
    </footer>
  </main>
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
            this.speechEvents.push({
              speaker: event.speakerName || 'Null',
              duration: Math.max((result[index + 1].timestamp - event.timestamp) / 1000, 0),
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
