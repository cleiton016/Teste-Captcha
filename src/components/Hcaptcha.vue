<script src="https://unpkg.com/vue"></script>
<script src="https://unpkg.com/@hcaptcha/vue-hcaptcha"></script>

<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <form v-on:submit.prevent='validarRecaptcha'>
      <label class="col-12 col-md-4" label="Critério de busca">
        <select v-model="form.criterio">
          <option v-for="(criterio, index) in criterios" :key="index" v-bind:value="criterio.value">
            {{ criterio.label }}
          </option>
        </select>
      </label>
      <div class="g-recaptcha" data-sitekey="6LeIxAcTAAAAAJcZVRqyHh71UMIEGNQ_MXjiZKhI"></div>
      <br>
      <vue-hcaptcha
            sitekey="10000000-ffff-ffff-ffff-000000000001"
            @verify="checkRecaptcha"
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
  name: 'Hcaptcha',
  components: { VueHcaptcha },
  props: {
    msg: String,
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
    onVerify: (token, eKey) => {console.log('Verified: ', {token, eKey})},
    onExpire: () => {console.log('Expired')},
    onError: (err) => {console.log('Error', err)},
    checkRecaptcha(response){
      alert("checkRecaptcha",{response})
      this.form.verificado = true;
      this.form.msgRecaptcha = 'Verificado'
    },
    validarRecaptcha(){
      alert("validarRecaptcha")
      if(!this.form.verificado){
        this.form.msgRecaptcha= "Valide o Recaptcha"
        return true
      }
    },
    async teste(){
      
    }
  }
}
</script>
