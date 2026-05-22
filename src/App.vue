<script setup>
import { ref, onMounted } from 'vue'
import ContactList from './components/ContactList.vue'
import ContactForm from './components/ContactForm.vue'

const contacts = ref([])
const selectedContact = ref(null)
const loading = ref(false)
const error = ref('')

const fetchContacts = async () => {
  loading.value = true
  try {
    const res = await fetch('http://localhost:3001/contacts')
    contacts.value = await res.json()
  } catch (err) {
    error.value = "Erreur chargement"
  }
  loading.value = false
}

onMounted(fetchContacts)

// ADD
const addContact = async (contact) => {
  await fetch('http://localhost:3001/contacts', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(contact)
  })
  fetchContacts()
}

// DELETE
const deleteContact = async (id) => {
  if (!confirm("Supprimer ?")) return

  await fetch(`http://localhost:3001/contacts/${id}`, {
    method: 'DELETE'
  })
  fetchContacts()
}

// SELECT FOR UPDATE
const selectContact = (contact) => {
  selectedContact.value = contact
}

// UPDATE
const updateContact = async (contact) => {
  await fetch(`http://localhost:3001/contacts/${contact.id}`, {
    method: 'PUT',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(contact)
  })
  selectedContact.value = null
  fetchContacts()
}
</script>

<template>
  <div class="container">
    <h1>Gestion Contacts</h1>

    <p v-if="loading" class="info">Chargement...</p>
    <p v-if="error" class="error">{{ error }}</p>

    <div class="form-section">
      <ContactForm 
        @add="addContact" 
        @update="updateContact"
        :selected="selectedContact"
      />
    </div>

    <div class="list-section">
      <ContactList 
        :contacts="contacts"
        @delete="deleteContact"
        @edit="selectContact"
      />
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 600px;
  margin: 40px auto;
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 2px 16px rgba(0,0,0,0.08);
  padding: 32px 24px 24px 24px;
  font-family: 'Segoe UI', Arial, sans-serif;
}
h1 {
  text-align: center;
  color: #2c3e50;
  margin-bottom: 24px;
}
.form-section {
  margin-bottom: 32px;
}
.list-section {
  margin-top: 16px;
}
.info {
  color: #2980b9;
  text-align: center;
}
.error {
  color: #e74c3c;
  text-align: center;
  font-weight: bold;
}
</style>
