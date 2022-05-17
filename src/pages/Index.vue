<template>
  <q-page class="container" padding>
    <p class="text-h4">Formulário</p>
    <div class="row q-col-gutter-md">
      <q-input
        outlined
        clearable
        v-model="form.nome"
        label="Nome"
        class="col-md-12 col-sm-12 col-xs-12"
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
      >
        <template v-slot:prepend>
          <q-icon name="mails" />
        </template>
      </q-input>

      <q-input
        v-model.number="form.telefone"
        outlined
        label="Telefone"
        class="col-md-12 col-sm-12 col-xs-12"
        mask="(##) #####-####"
        unmasked-value
      />
    </div>
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
      },
    };
  },
});
</script>
s
