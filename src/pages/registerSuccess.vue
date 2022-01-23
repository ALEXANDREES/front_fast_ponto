<template>
  <div class="fullscreen bg-primary text-white text-center q-pa-md flex flex-center">
    <div>
      <div class="text-h3">
        Cadastro realizado com sucesso!
      </div>

      <div class="text-h4" style="opacity:.4">
        Seja bem vindo a plataforma
      </div>

      <q-btn
        class="q-mt-xl"
        color="white"
        text-color="primary"
        unelevated
        to="/"
        label="Home"
        no-caps
      />
    </div>
  </div>
</template>

<script>

export default {
  name: 'registerSuccess'
}
</script>
