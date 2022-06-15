<template>
  <main>
    <Navbar />
    <div class="container">
      <div class="section">
        <h1 class="title">
          Social VR - Time Management Tool
        </h1>
        <div class="field">
          <textarea v-model="input" spellcheck="false" class="textarea" :class="{ 'is-danger': error.length > 0}" placeholder="Paste study data here" />
          <p v-show="error.length > 0" class="help is-danger">
            {{ error }}
          </p>
        </div>
        <div class="field">
          <button class="button is-primary is-fullwidth" @click="display">
            Display
          </button>
        </div>
      </div>
      <div v-if="processed">
        <div class="section">
          <h2 class="subtitle">
            Meta Info
          </h2>
          <ul>
            <li>Started: {{ new Date(started).toLocaleString() }}</li>
            <li>Completed: {{ new Date(completed).toLocaleString() }}</li>
          </ul>
        </div>

        <div class="section">
          <div class="columns">
            <div class="column">
              <h2 class="subtitle">
                Knowledge
              </h2>
              <ul>
                <li v-for="(ksa, index) in knowledge" :key="index">
                  <div class="tag is-info is-normal">
                    {{ ksa }}
                  </div>
                </li>
              </ul>
            </div>
            <div class="column">
              <h2 class="subtitle">
                Skills
              </h2>
              <ul>
                <li v-for="(ksa, index) in skills" :key="index">
                  <div class="tag is-link is-normal">
                    {{ ksa }}
                  </div>
                </li>
              </ul>
            </div>
            <div class="column">
              <h2 class="subtitle">
                Abilities
              </h2>
              <ul>
                <li v-for="(ksa, index) in abilities" :key="index">
                  <div class="tag is-success is-normal">
                    {{ ksa }}
                  </div>
                </li>
              </ul>
            </div>
          </div>
        </div>

        <div class="section">
          <h2 class="subtitle">
            Canidate
          </h2>
          <ul>
            <li class="has-text-weight-semibold">
              {{ canidate }}
            </li>
          </ul>
        </div>
      </div>
    </div>
    <Footer />
  </main>
</template>

<script>
export default {
  data () {
    return {
      input: '',
      started: -1,
      completed: -1,
      knowledge: ['', '', ''],
      skills: ['', '', ''],
      abilities: ['', '', ''],
      canidate: '',
      processed: false,
      error: ''
    }
  },

  methods: {
    display () {
      try {
        const parsed = JSON.parse(this.input)

        this.started = parsed.started_at
        this.completed = parsed.completed_at
        this.knowledge = [...parsed.knowledge]
        this.skills = [...parsed.skills]
        this.abilities = [...parsed.abilities]
        this.canidate = parsed.canidate

        this.processed = true
      } catch (e) {
        this.error = e.toString()
      }
    }
  }
}
</script>
