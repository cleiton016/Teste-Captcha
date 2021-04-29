<template>
    <div class="hello">
        <h1>{{ msg }}</h1>
        <form v-on:submit.prevent="validarRecaptcha">
        <label label="Critério de busca">
            <select v-model="form.criterio" required>
            <option v-for="(criterio, index) in criterios" :key="index" v-bind:value="criterio.value">
                {{ criterio.label }}
            </option>
            </select>
        </label>
        
        <label label="Buscar">
            <input v-model="form.busca">
        </label>
        <br>
        <vue-recaptcha @verify="checkRecaptcha" @expired="invalidar"
            sitekey="6LenD7waAAAAAFYUiifS2QE6dWD3qnQhMK8fCAhL" >
        </vue-recaptcha>
        <button>submit</button>
        <div><strong>{{ form.msgRecaptcha }}</strong></div>
        </form>
    </div>
    
</template>



<script>
import VueRecaptcha from 'vue-recaptcha';

export default {
    name: 'Recaptcha',
    components: { VueRecaptcha },
    props: {
        msg: String,
    },
    data() {
        return {
            buscaRealizada: false,
            loading: false,
            form: {
                verificado:false,
                msgRecaptcha: "Teste",
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
        checkRecaptcha(response){
            alert(response)
            this.form.verificado = true;
            this.form.msgRecaptcha = 'Verificado'
        },
        invalidar(){
            this.form.verificado = false;
            this.form.msgRecaptcha = 'Expirado'
        },
        validarRecaptcha(){
            if(!this.form.verificado){
                this.form.msgRecaptcha= "Valide o Recaptcha"
                return true
            }
            localStorage.setItem(this.form.criterio, this.form.busca)
        }
    }
}
</script>

