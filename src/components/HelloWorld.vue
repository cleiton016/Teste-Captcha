<script src="https://unpkg.com/vue"></script>
<script src="https://unpkg.com/@hcaptcha/vue-hcaptcha"></script>

<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <form @submit='teste'>
      <label class="col-12 col-md-4" label="Critério de busca">
        <select v-model="form.criterio">
          <option v-for="(criterio, index) in criterios" :key="index" v-bind:value="criterio.value">
            {{ criterio.label }}
          </option>
        </select>
      </label>
      <vue-hcaptcha
            sitekey="10000000-ffff-ffff-ffff-000000000001"
            @verify="onVerify"
            @expired="onExpire"
            @challengeExpired="onExpire"
            @error="onError"
      ></vue-hcaptcha>
      <div>
        <input type="submit" value="Submit">
      </div>
    </form>
  </div>

</template>



<script>
import VueHcaptcha from '@hcaptcha/vue-hcaptcha';
export default {
  name: 'HelloWorld',
  components: { VueHcaptcha },
  props: {
    msg: String
  },
  data() {
        return {
            buscaRealizada: false,
            loading: false,
            captcha: null,
            form: {
                criterio: null,
                busca: '',
            },
            criterios: [
                { label: 'Código do imóvel', value: 'cod_imovel' },
                { label: 'Número do protocolo SICAR', value: 'cod_protoc' },
                { label: 'CPF do Explorador/Proprietário', value: 'cpf_cnpj' },
                { label: 'Token da propriedade', value: 'token' },
            ],
        };
    },
  methods:{
    onVerify: (token, eKey) => {
      console.log('Verified: ', {token, eKey})
    },
    onExpire: () => {
      this.captcha = fasle
      console.log('Expired')
    },
    onError: (err) => {
      this.captcha = false
      console.log('Error', err)
    },
    teste(){
    setTimeout(alert(this.captcha), 3000)
    this.msg = "Verificado"
    
    
    }
  }
}
</script>
