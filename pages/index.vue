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
        <div v-show="speechEvents.length > 0" class="field">
          <button class="button is-info is-fullwidth" :disabled="summed" @click="sum">
            Get Total Time
          </button>
        </div>
        <div class="field">
          <label class="checkbox is-unselectable">
            <input v-model="removeNull" type="checkbox">
            Remove Null references
          </label>
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
      speechEvents: [],
      summed: false,
      removeNull: true
    }
  },

  methods: {
    convert () {
      try {
        this.speechEvents = []
        this.error = ''
        this.summed = false

        const parsed = JSON.parse(this.input)
        const filtered = []

        parsed
          .filter((e) => {
            return e.eventType === 'startSpeech' || e.eventType === 'stopSpeech'
          })
          .forEach((e, index) => {
            if (this.removeNull && e.speakerName == null) {
              return
            }

            if (index < parsed.length - 1) {
              filtered.push({
                speaker: `${e.speakerName}`,
                duration: (parsed[index + 1].timestamp - e.timestamp) / 1000,
                key: Math.floor(Math.random() * Date.now())
              })
            }
          })

        this.speechEvents = JSON.parse(JSON.stringify(filtered))
      } catch (e) {
        this.error = e.toString()
      }
    },

    sum () {
      this.speechEvents = JSON.parse(JSON.stringify(Array.from(this.speechEvents.reduce((m, { speaker, duration }) => m.set(speaker, (m.get(speaker) || 0) + duration), new Map()), ([speaker, duration]) => ({ speaker, duration }))))
      this.summed = true
    }
  }
}
</script>
