<template>
  <div>
    <section class="hero is-bold" :class="{'is-info': estimatedWaiting > 45, 'is-success': estimatedWaiting <= 45}">
      <div class="hero-body">
        <div class="container" style="text-align: center;">
          <p class="title is-3">
            Your position in queue:
          </p>
          <p class="title is-2">
            {{ position }}
          </p>
          <p class="subtitle">
            Estimated time:<br>{{ estimatedWaitingHuman }}
          </p>
        </div>
      </div>
    </section>

    <section class="section content">
      <h4 class="title is-4">
        Entry form
      </h4>
      <p>
        You may fill out entry form digitally to make the process faster
      </p>
      <div class="buttons">
        <button class="button is-success is-medium" @click="isFormModal = !isFormModal">
          Fill out the form
        </button>
      </div>

      <h4 class="title is-4">
        Security code
      </h4>
      <p>
        This secuirty codes should be kept as a secret and provided <b><u>only</u></b> for <b>border control officers</b>.
      </p>
      <div class="buttons">
        <button class="button is-danger" @click="isSecurityModal = !isSecurityModal">
          Show security code
        </button>
      </div>

      <b-modal :active.sync="isFormModal" :width="350" scroll="keep">
        <div class="card">
          <div class="card-content">
            <div class="content">
              <h4 class="title is-4">
                Entry form
              </h4>

              <b-field label="Name">
                <b-input type="text" />
              </b-field>

              <b-field label="Surname">
                <b-input type="text" />
              </b-field>

              <b-field label="Age">
                <b-input type="number" />
              </b-field>

              <b-field label="Nationality">
                <b-input type="number" />
              </b-field>

              <b-field label="ID number">
                <b-input type="number" />
              </b-field>

              <b-field label="Quarantine facility address">
                <b-input type="number" />
              </b-field>

              <div class="field">
                <b-switch>Did you visit China this year?</b-switch>
              </div>

              <div class="field">
                <b-switch>Have you had a fever in the last 7 days?</b-switch>
              </div>

              <button class="button is-success" @click="isFormModal = false">
                Update
              </button>
            </div>
          </div>
        </div>
      </b-modal>

      <b-modal :active.sync="isSecurityModal" :width="350" scroll="keep">
        <div class="card">
          <div class="card-content">
            <div class="content">
              <h4 class="title is-4">
                Secuirty code
              </h4>

              <h3 class="title is-5">
                Your security code: {{ securityCode }}
              </h3>

              <button class="button is-dark" @click="isSecurityModal = false">
                Close
              </button>
            </div>
          </div>
        </div>
      </b-modal>
    </section>
  </div>
</template>

<script>
export default {
  data: () => ({
    position: 26,
    changeInterval: null,
    isFormModal: false,
    isSecurityModal: false
  }),
  computed: {
    estimatedWaiting () {
      return (this.position * 5) * 0.85
    },
    estimatedWaitingHuman () {
      if (this.estimatedWaiting < 60) {
        return `${Math.round(this.estimatedWaiting)} minutes`
      } else {
        const hours = Math.floor(this.estimatedWaiting / 60)
        const fraction = (this.estimatedWaiting / 60) % 1

        if (fraction < 0.25) {
          return `${hours} hours`
        } else if (fraction < 0.5) {
          return `${hours} hours 15 minutes`
        } else if (fraction < 0.75) {
          return `${hours} hours 30 minutes`
        } else { return `${hours} hours 45 minutes` }
      }
    },
    securityCode () {
      return '27423309'
    }
  },
  mounted () {
    this.changeInterval = setInterval(() => {
      this.position--

      if (this.position === 5) {
        this.$buefy.dialog.alert('Please head towards the border control station')
      }

      if (this.position < 1) { clearInterval(this.changeInterval) }
    }, 2000)
  },
  beforeDestroy () {
    clearInterval(this.changeInterval)
  }
}
</script>
