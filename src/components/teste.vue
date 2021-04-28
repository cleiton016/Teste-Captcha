<template>
    <q-page padding class="s-container">
        <s-card v-if="$can('VISUALIZAR', 'PROPRIEDADES')" title="Busca de propriedades rurais">
            <q-card-section>
                <q-form @submit="search" class="row items-center q-col-gutter-x-md">
                    <s-label class="col-12 col-md-4" label="Critério de busca">
                        <q-select outlined dense v-model="form.criterio" :options="criterios" lazy-rules :
                            rules="[ val => $v.form.criterio.required || 'Selecione um critério de busca' ]"/>
                    </s-label>
                    <s-label class="col-12 col-md-5" label="Busca">
                        <q-input 
                            outlined
                            dense: value="form.busca | cpfCnpj" 
                            @input="form.busca = removeSymbols($event)"
                            v-if="form.criterio && form.criterio.value === 'cpf_cnpj'" 
                                maxlength="18" lazy-rules: rules="[
                                    val => $v.form.busca.required || 'Este campo é obrigatório',
                                    val => [11,14].includes(removeSymbols(val).length)
                                    || 'Insira um documento válido',]"
                        />
                        <q-input
                            outlined
                            dense
                            v-model="form.busca"
                            v-else
                            lazy-rules
                            :rules="[
                            val => $v.form.busca.required || 'Este campo é obrigatório',
                            ]"
                        />
                    </s-label>
                    <q-space></q-space>
                    <div>
                    <q-btn no-caps rounded color="primary" type="submit">Buscar propriedade</q-btn>
                    </div>
                </q-form>
                <q-separator />
            </q-card-section>
        </s-card>
    </q-page>
</template>

<script>
export default {
    name: 'PropriedadesBuscaPage',
    components: {
        
    },
    filters: {
    },
    data() {
        return {
            buscaRealizada: false,
            loading: false,
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
    computed: {

    },
    
    methods: {
        async search() {

        },
    },
    };
</script>

