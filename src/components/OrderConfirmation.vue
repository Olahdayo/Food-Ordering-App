<template>
  <div class="modal-backdrop">
    <div class="modal-content">
      <h4>Confirm Order</h4>
      <p>Are you sure you want to place the order?</p>
      <button class="btn btn-primary" @click="$emit('confirm')">
        Yes, Place Order
      </button>
      <button class="btn btn-secondary" @click="$emit('cancel')">Cancel</button>
    </div>
  </div>
</template>

<script>
export default {};
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
  text-align: center;
}
</style>
