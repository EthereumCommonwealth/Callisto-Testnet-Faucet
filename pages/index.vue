<template>
  <div class="container">
    <div>
      <Logo />
      <div class="row">
        <div class="col-12">
          <h1 class="title">
            Testnet Faucet
          </h1>
        </div>
      </div>

      <div class="row">
        <div class="col-12">
          <b-form @submit="onSubmit">
            <b-form-group
              id="input-group-1"
              label="Callisto address:"
              label-for="input-1"
              description="Put your Callisto Testnet address to receive CLO."
            >
              <b-form-input
                id="input-1"
                v-model="form.address"
                placeholder="Enter your CLO Address"
                required
              />
            </b-form-group>

            <b-button type="submit" variant="primary">
              Get Testnet CLO
            </b-button>
          </b-form>
          <b-card class="mt-3" header="Request Result">
            <pre class="m-0">{{ reqResult }}</pre>
          </b-card>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      form: {
        address: ''
      },
      reqResult: ''
    }
  },
  methods: {
    async onSubmit (event) {
      event.preventDefault()
      try {
        this.reqResult = await this.$axios.$post('https://testnet-faucet.callisto.network/', this.form.address)
      } catch (error) {
        console.log(error)
        this.reqResult = error.response.data
      }
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}
</style>
