<script setup>
import { RouterLink } from "vue-router";
</script>

<template>
  <div>
    <div>
      <RouterLink
       :to="{ name: 'inicio' }"
       class="block md:inline-block rounded bg-blue-600 py-2 px-3"
       > Volver </RouterLink>
    </div>
    <h1 class="text-4xl font-extrabold text-slate-500">Agregar Cliente</h1>
  </div>
</template>
