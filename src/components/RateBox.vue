<template>
  <div class="rate-box">
    <template v-if="editable">

      <span v-for="star in 5" :key="star" class="star editable"
        :class="{ filled: star <= (hoveredStar || internalValue) }" @mouseover="onMouseOver(star)"
        @mouseout="onMouseOut" @click="onClick(star)">
        ★
      </span>
    </template>
    <template v-else>

      <span v-for="star in 5" :key="star" class="star" :class="{ filled: star <= internalValue }">
        ★
      </span>
    </template>
  </div>
</template>

<script setup>
import { ref, defineProps, defineEmits, watch, onMounted } from 'vue';

const props = defineProps({
  modelValue: {
    type: Number,
    required: true,
  },
  editable: {
    type: Boolean,
    default: true,
  },
  defaultValue: {
    type: Number,
    default: 0,
  },
});

const emit = defineEmits(['update:modelValue']);
const hoveredStar = ref(null);
const internalValue = ref(props.modelValue || props.defaultValue);

onMounted(() => {
  if (props.modelValue === 0 && props.defaultValue !== 0) {
    emit('update:modelValue', props.defaultValue);
  }
});

watch(() => props.modelValue, (newValue) => {
  internalValue.value = newValue;
});

const onMouseOver = (star) => {
  if (props.editable) {
    hoveredStar.value = star;
  }
};

const onMouseOut = () => {
  if (props.editable) {
    hoveredStar.value = null;
  }
};

const onClick = (star) => {
  if (props.editable) {
    const newValue = props.modelValue === star ? 0 : star;
    emit('update:modelValue', newValue);
  }
};
</script>

<style scoped>
.rate-box {
  display: inline-flex;
}

.star {
  font-size: 2rem;
  color: #ccc;
}

.star.editable {
  cursor: pointer;
}

.star.filled {
  color: #f39c12;
}

.star.editable:hover {
  color: #f39c12;
}
</style>