<template>
  <Teleport to="body">
    <div class="modal-backdrop">
      <div class="modal-content">
        <h4>{{ dish.name }}</h4>
        <p>{{ dish.description }}</p>
        <p><strong>Price:</strong> ${{ dish.price.toFixed(2) }}</p>
        <button class="btn btn-secondary" @click="$emit('close')">Close</button>
      </div>
    </div>
  </Teleport>
</template>

<script>
export default {
  props: ["dish"],
};
</script>

<style>
.modal-backdrop {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background: #fff;
  padding: 20px;
  border-radius: 5px;
  width: 300px;
}
</style>
