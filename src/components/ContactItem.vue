<script setup>
defineProps(['contact'])
const emit = defineEmits(['delete', 'edit'])
</script>

<template>
  <div class="contact-card">
    <div class="info">
      <p class="name">{{ contact.name }}</p>
      <p class="email">{{ contact.email }}</p>
      <p class="phone">{{ contact.phone }}</p>
    </div>
    <div class="actions">
      <button class="edit-btn" @click="emit('edit')">Modifier</button>
      <button class="delete-btn" @click="emit('delete')">Supprimer</button>
    </div>
  </div>
</template>

<style scoped>
.contact-card {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #f4f8fb;
  border-radius: 8px;
  box-shadow: 0 1px 4px rgba(0,0,0,0.04);
  padding: 14px 18px;
  margin-bottom: 12px;
  transition: box-shadow 0.2s;
}
.contact-card:hover {
  box-shadow: 0 4px 16px rgba(41,128,185,0.10);
}
.info .name {
  font-weight: bold;
  color: #2c3e50;
  margin-bottom: 2px;
}
.info .email, .info .phone {
  color: #555;
  font-size: 0.97rem;
  margin-bottom: 0;
}
.actions {
  display: flex;
  gap: 8px;
}
.edit-btn {
  background: #27ae60;
  color: #fff;
  border: none;
  border-radius: 4px;
  padding: 6px 12px;
  cursor: pointer;
  font-size: 0.97rem;
  transition: background 0.2s;
}
.edit-btn:hover {
  background: #219150;
}
.delete-btn {
  background: #e74c3c;
  color: #fff;
  border: none;
  border-radius: 4px;
  padding: 6px 12px;
  cursor: pointer;
  font-size: 0.97rem;
  transition: background 0.2s;
}
.delete-btn:hover {
  background: #c0392b;
}
</style>
