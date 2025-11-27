<script setup>
defineProps(['count']);
</script>

<template>
    <header class="header">
        <h1>Cooking Masterclass</h1>
        <div class="wishlist-status">
            ❤️ Wishlist: <strong>{{ count }}</strong> items
        </div>
    </header>
</template>

<style scoped>
.header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #fff;
    padding: 15px 20px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 8px;
}

.wishlist-status {
    font-weight: bold;
    color: #ff6347;
}
</style>