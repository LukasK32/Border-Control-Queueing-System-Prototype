<template>
  <div>
    <section class="hero is-info is-bold">
      <div class="hero-body">
        <div class="container">
          <p class="title">
            Hello!
          </p>
          <p class="subtitle">
            This is a queueing system for border control
          </p>
        </div>
      </div>
    </section>

    <div class="section content">
      <h4 class="title is-4">
        Join queue
      </h4>
      <p>
        Join queue by scanning QR code or by entering PIN code provided by border control officers or volounteers
      </p>
      <div class="buttons">
        <button class="button is-medium" :class="{'is-loading': codeLoading, 'is-success': !codeDisabled, 'is-warning': codeDisabled}" :disabled="codeDisabled" @click="scanCode">
          Scan QR code
        </button>
        <button class="button is-success is-medium" @click="isPinModalEnabled = !isPinModalEnabled">
          Enter PIN code
        </button>
      </div>

      <h4 class="title is-4">
        Informations
      </h4>

      <div class="buttons">
        <button class="button is-info is-medium" @click="isStatusModalEnabled = !isStatusModalEnabled">
          Current pandemic status
        </button>
        <button class="button is-dark is-medium" @click="isPrivacyModalEnabled = !isPrivacyModalEnabled">
          Privacy policy
        </button>
      </div>

      <b-modal :active.sync="isPinModalEnabled" :width="350" scroll="keep">
        <div class="card">
          <div class="card-content">
            <div class="content">
              <h4 class="title is-4">
                Enter PIN code
              </h4>
              <p>
                Enter PIN code provided by border control officers or volounteers
              </p>
              <p>
                <b-field label="PIN (correct: 2897)">
                  <b-input v-model="pin" type="number" />
                </b-field>
                <button class="button is-success" @click="enterQueue">
                  Enter the queue
                </button>
              </p>
            </div>
          </div>
        </div>
      </b-modal>

      <b-modal :active.sync="isPrivacyModalEnabled" :width="350" scroll="keep">
        <div class="card">
          <div class="card-content">
            <div class="content">
              <h4 class="title is-4">
                Privacy policy
              </h4>
              <h5 class="title is-5">
                Lorem ipsum dolor
              </h5>
              <p>
                Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec mi nisl, egestas eu iaculis imperdiet, blandit vel quam. Quisque arcu mi, dictum quis massa ac, vehicula mollis tortor. Proin mauris eros, tempor at ipsum vel, blandit commodo justo. Phasellus dui risus, eleifend ac arcu vel, gravida tempus neque. Donec justo nulla, rutrum sed imperdiet sed, ultrices vel est. Morbi maximus nisi mauris, at euismod felis feugiat vitae. Sed in ultrices lorem. Proin ullamcorper neque nibh, eget cursus risus dapibus non. Nam vel nisl tincidunt, elementum quam eget, porttitor magna. Mauris non nisi eu orci sagittis vestibulum. Curabitur consequat erat bibendum sapien sodales, vel porttitor nulla auctor. Maecenas hendrerit risus erat, vel luctus quam sodales id. Mauris tincidunt sapien et nulla elementum, id facilisis augue interdum.
              </p>
              <h5 class="title is-5">
                Vivamus feugiat
              </h5>
              <p>
                Vivamus feugiat, lacus vel aliquam cursus, diam ante bibendum nibh, nec malesuada velit nibh nec metus. Phasellus efficitur elit vitae tincidunt malesuada. Morbi sagittis ullamcorper egestas. Quisque facilisis lobortis mauris id vestibulum. Donec et dapibus sem. Praesent efficitur, erat a condimentum viverra, nisi diam tristique lacus, sit amet tincidunt tellus orci quis justo. Pellentesque blandit leo ut purus eleifend, eget molestie diam tincidunt. In vulputate finibus enim vel venenatis.
              </p>
              <h5 class="title is-5">
                Nam tristique iaculis
              </h5>
              <p>
                Nam tristique iaculis ante ac pretium. Maecenas lobortis ante a sem rhoncus interdum. Nunc eget magna sit amet elit maximus vulputate. Proin nisl arcu, porttitor non auctor vitae, condimentum nec tortor. Aliquam bibendum sodales diam, et egestas nibh sollicitudin posuere. Morbi ac dignissim mi. Donec nec est consequat, ullamcorper mauris eget, blandit orci.
              </p>
            </div>
          </div>
        </div>
      </b-modal>

      <b-modal :active.sync="isStatusModalEnabled" :width="350" scroll="keep">
        <div class="card">
          <div class="card-content">
            <div class="content">
              <h4 class="title is-4">
                Pandemic status
              </h4>
              <h5 class="title is-5">
                Latest announcement
              </h5>
              <p>
                Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec mi nisl, egestas eu iaculis imperdiet, blandit vel quam. Quisque arcu mi, dictum quis massa ac, vehicula mollis tortor.
              </p>
              <h5 class="title is-5">
                More informations
              </h5>
              <a class="button is-info" href="https://www.who.int/health-topics/coronavirus" target="_blank">
                WHO
              </a>
              <a class="button is-info" href="https://www.gov.pl/web/coronavirus" target="_blank">
                GOV.pl
              </a>
            </div>
          </div>
        </div>
      </b-modal>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomePage',
  data: () => ({
    codeLoading: false,
    codeDisabled: false,
    isPinModalEnabled: false,
    isPrivacyModalEnabled: false,
    isStatusModalEnabled: false,
    pin: 0
  }),
  methods: {
    scanCode () {
      if (this.codeLoading || this.codeDisabled) { return }

      this.codeLoading = true

      setTimeout(() => {
        this.codeLoading = false
        this.codeDisabled = true

        this.$buefy.toast.open({
          duration: 5000,
          message: 'Your device does not support QR code scanning',
          position: 'is-top',
          type: 'is-danger'
        })
      }, 1500)
    },
    enterQueue () {
      if (parseInt(this.pin) !== 2897) {
        this.$buefy.toast.open({
          duration: 5000,
          message: 'Incorrect PIN code',
          position: 'is-top',
          type: 'is-danger'
        })
      } else {
        this.$router.push('/queue')
      }
    }
  }
}
</script>
