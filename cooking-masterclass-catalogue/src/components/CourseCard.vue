<script setup>
import { ref } from 'vue';

const props = defineProps(['course']);

const emit = defineEmits(['add-to-wishlist']);

const isSaved = ref(false);

const toggleSave = () => {
    if (props.course.available) {
        isSaved.value = !isSaved.value;
        emit('add-to-wishlist', isSaved.value);
    }
};

const formattedPrice = props.course.price.toFixed(2);
</script>

<template>
    <div :class="['course-card', { 'sold-out': !course.available }]">
        <h2>{{  course.title  }}</h2>
        <p><strong>Chef:</strong> {{ course.chef }}</p>
        <p><strong>Level:</strong> {{ course.level }}</p>
        <div class="status-section">
            <span v-if="course.available" class="available-status">Available</span>
            <span v-else class="sold-out-status">Sold Out</span>
        </div>

        <div class="actions">
            <span class="price">${{ formattedPrice }}</span>
            <button
                @click="toggleSave"
                :disabled="!course.available"
                :class="{ 'saved': isSaved }"
            >
                {{ isSaved ? 'Saved! ⭐' : 'Save to wishlist' }}
            </button>
        </div>
    </div>
</template>

<style scoped>
.course-card {
    background-color: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    transition: transform 0.2s;
    display: flex;
    flex-direction: column;
}

.course-card:hover {
    transform: translateY(-5px);
}

.course-card.sold-out {
    opacity: 0.6;
    background-color: #fdd;
}

h2 {
    color: #333;
    margin-top: 0;
}

.status-section {
    margin-bottom: 15px;
}

.available-status {
    color: #28a745;
    font-weight: bold;
}

.sold-out-status {
    color: #dc3545;
    font-weight: bold;
}

.actions {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: auto;
    padding-top: 15px;
    border-top: 1px solid #eee;
}

.price {
    font-size: 1.5em;
    font-weight: bold;
    color: #007bff;
}

button {
    background-color: #ff6347;
    color: white;
    border: none;
    padding: 10px 15px;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.2s;
}

button:hover:enabled {
    background-color: #e55337;
}

button:disabled {
    cursor: not-allowed;
    background-color: #aaa;
}

button.saved {
    background-color: #28a745;
}
</style>