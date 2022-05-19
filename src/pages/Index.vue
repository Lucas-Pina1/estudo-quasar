<template>
  <q-page class="container" padding>
    <p class="text-h4">Formulário</p>
    <q-form
      @submit="onSubmit"
      @reset="onReset"
      class="row q-col-gutter-md"
      ref="myform"
    >
      <q-input
        outlined
        clearable
        v-model="form.nome"
        label="Nome"
        class="col-md-12 col-sm-12 col-xs-12"
        :rules="[(val) => (val && val.length > 0) || 'Nome obrigatório']"
      >
        <template v-slot:prepend>
          <q-icon name="person" />
        </template>
      </q-input>

      <q-input
        v-model.number="form.idade"
        type="number"
        outlined
        label="Idade"
        class="col-md-12 col-sm-12 col-xs-12"
        :rules="[
          (val) => (val !== null && val !== '') || 'Idadde obrigatória',
          (val) => (val > 0 && val < 100) || 'Coloque uma idade real',
        ]"
      >
        <template v-slot:prepend>
          <q-icon name="person" />
        </template>
      </q-input>

      <q-input
        v-model.number="form.email"
        outlined
        label="Email"
        suffix="@gmail.com"
        class="col-md-12 col-sm-12 col-xs-12"
        :rules="[
          (val) => (val && val.length > 0) || 'Email obrigatório',
          (val) => validareEmail(val) || 'Coloque um email valido',
        ]"
      >
        <template v-slot:prepend>
          <q-icon name="email" />
        </template>
      </q-input>

      <q-input
        v-model="form.telefone"
        outlined
        label="Telefone"
        class="col-md-12 col-sm-12 col-xs-12"
        placeholder="(xx) xxxxx-xxxx"
        mask="(##) #####-####"
        unmasked-value
        :rules="[
          (val) => (val && val.length > 0) || 'Telefone obrigatório',
          (val) => val.length === 11 || 'Coloque um telefone real',
        ]"
      />
      <q-select
        outlined
        v-model="form.tipoPessoa"
        :options="optionsTipoPesoas"
        label="Tipo de pessoa"
        emit-value
        map-options
        class="col-md-12 col-sm-12 col-xs-12"
        :rules="[
          (val) => (val && val.length > 0) || 'Tipo de pessoa obrigatório',
        ]"
      />

      <span class="text-bold">Sexo:</span>
      <q-option-group
        :options="optionsSexo"
        label="Sexo"
        type="radio"
        v-model="form.sexo"
        class="col-md-12 col-sm-12 col-xs-12"
      />

      <span class="text-bold">Possui dificuldades?</span>
      <q-option-group
        :options="optionsDificuldades"
        label="Dificuldades"
        type="checkbox"
        v-model="form.dificuldades"
        class="col-md-12 col-sm-12 col-xs-12"
      />

      <q-toggle
        label="Receber notificações?"
        color="primary"
        icon="mail"
        v-model="form.notificacoes"
        size="lg"
      />

      <div class="col-12">
        <q-btn
          label="Cadastrar"
          type="submit"
          color="primary"
          class="float-right"
        />
        <q-btn
          label="Resetar"
          type="reset"
          color="default"
          text-color="black"
          class="float-right q-mr-md"
        />
      </div>
    </q-form>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "PageIndex",
  data() {
    return {
      form: {
        nome: "",
        idade: "",
        email: "",
        telefone: "",
        tipoPessoa: "",
        sexo: "NI",
        dificuldades: [],
        notificacoes: false,
      },
      optionsTipoPesoas: [
        { label: "Pessoa Física", value: "pf" },
        { label: "Pessoa Jurídica", value: "pj" },
      ],
      optionsSexo: [
        { label: "Não informado", value: "NI" },
        { label: "Masculino", value: "M" },
        { label: "Feminino", value: "F" },
      ],
      optionsDificuldades: [
        { label: "Motoras", value: "motoras" },
        { label: "Visuais", value: "visuais" },
        { label: "Respiratórias", value: "respiratorias" },
        { label: "Não", value: "Não" },
      ],
    };
  },
  methods: {
    validareEmail(email) {
      return /[a-z0-9]+@[a-z]+\.[a-z]{2,3}/.test(email);
    },
    onSubmit() {
      this.$q.notify({
        message: "Cadastro realizado com sucesso",
        color: "positive",
        icon: "check_circle_outline",
      });
      this.onReset();
    },
    async onReset() {
      await this.resetForm();
      this.$refs.myForm.resetValidation();
    },
    async resetForm() {
      this.form = {
        nome: "",
        idade: "",
        email: "",
        telefone: "",
        tipoPessoa: "",
        sexo: "NI",
        dificuldades: [],
        notificacoes: false,
      };
    },
  },
});
</script>
