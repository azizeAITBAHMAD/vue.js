<script setup>
import ContactItem from './ContactItem.vue'

defineProps(['contacts'])
const emit = defineEmits(['delete', 'edit'])
</script>

<template>
  <div>
    <h2>Liste</h2>

    <p v-if="contacts.length === 0">Aucun contact</p>

    <ContactItem 
      v-for="c in contacts"
      :key="c.id"
      :contact="c"
      @delete="emit('delete', c.id)"
      @edit="emit('edit', c)"
    />
  </div>
</template>
