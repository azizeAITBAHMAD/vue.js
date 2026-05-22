<script setup>
import { ref, watch } from 'vue'

const props = defineProps(['selected'])
const emit = defineEmits(['add', 'update'])

const name = ref('')
const email = ref('')
const phone = ref('')

// remplir formulaire si update
watch(() => props.selected, (val) => {
  if (val) {
    name.value = val.name
    email.value = val.email
    phone.value = val.phone
  }
})

// submit
const submit = () => {
  if (!name.value || !email.value || !phone.value) {
    alert("Tous les champs sont obligatoires")
    return
  }

  if (props.selected) {
    emit('update', {
      id: props.selected.id,
      name: name.value,
      email: email.value,
      phone: phone.value
    })
  } else {
    emit('add', {
      name: name.value,
      email: email.value,
      phone: phone.value
    })
  }

  // reset
  name.value = ''
  email.value = ''
  phone.value = ''
}
</script>

<template>
  <div class="contact-form">
    <h2>{{ selected ? "Modifier" : "Ajouter" }}</h2>

    <div class="fields">
      <input v-model="name" placeholder="Nom" />
      <input type="email" v-model="email" placeholder="Email" />
      <input type="number" v-model="phone" placeholder="Téléphone" />
    </div>

    <button class="submit-btn" @click="submit">
      {{ selected ? "Update" : "Add" }}
    </button>
  </div>
</template>

<style scoped>
.contact-form {
  background: #f8f9fa;
  border-radius: 8px;
  padding: 20px 18px 16px 18px;
  box-shadow: 0 1px 4px rgba(0,0,0,0.04);
}
.contact-form h2 {
  margin-bottom: 16px;
  color: #34495e;
  font-size: 1.2rem;
}
.fields {
  display: flex;
  gap: 10px;
  margin-bottom: 12px;
}
.fields input {
  flex: 1;
  padding: 8px 10px;
  border: 1px solid #d1d5db;
  border-radius: 4px;
  font-size: 1rem;
  background: #fff;
  transition: border 0.2s;
}
.fields input:focus {
  border: 1.5px solid #2980b9;
  outline: none;
}
.submit-btn {
  background: #2980b9;
  color: #fff;
  border: none;
  border-radius: 4px;
  padding: 8px 18px;
  font-size: 1rem;
  cursor: pointer;
  transition: background 0.2s;
}
.submit-btn:hover {
  background: #1c5d85;
}
</style>
