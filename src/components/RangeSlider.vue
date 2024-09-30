<script setup>
import { ref, onMounted, computed } from "vue";
import MultiRangeSlider from "multi-range-slider-vue";

const props = defineProps(["min", "max", "step", "unit"]);
// Slider values
const min = ref(Number(props.min));
const max = ref(Number(props.max));

function updateValues(e) {
  min.value = e.minValue;
  max.value = e.maxValue;
}

const computedMin = computed({
  // getter
  get() {
    return min.value.toString();
  },
  // setter
  set(newValue) {
    // Note: we are using destructuring assignment syntax here.
    min.value = Number(newValue);
  },
});

const computedMax = computed({
  // getter
  get() {
    return max.value.toString();
  },
  // setter
  set(newValue) {
    // Note: we are using destructuring assignment syntax here.
    max.value = Number(newValue);
  },
});
</script>

<template>
  <MultiRangeSlider
    :min="Number(props.min)"
    :max="Number(props.max)"
    :step="Number(props.step)"
    :ruler="true"
    :label="true"
    :minValue="min"
    :maxValue="max"
    @input="updateValues"
  />
  <span class="aside_slider_text">
    <span class="aside_slider_text_selection">
      od
      <input
        type="number"
        class="aside_slider_text_input"
        v-model="computedMin"
      />
      {{ props.unit }}
    </span>

    <span class="aside_slider_text_selection">
      do
      <input
        type="number"
        class="aside_slider_text_input"
        v-model="computedMax"
      />
      {{ props.unit }}
    </span>
  </span>
</template>

<style lang="scss">
.multi-range-slider .thumb::before {
  background-color: var(--color-primary);
  border: none;
  box-shadow: none;
  margin-left: -8px;
  margin-top: -5px;
  border: solid 1px var(--color-white-1);
  width: 18px;
  height: 18px;
}

.multi-range-slider .ruler .ruler-rule {
  border-left: solid 1px var(--color-primary);
}

.multi-range-slider .ruler .ruler-rule:last-child {
  border-right: solid 1px var(--color-primary);
}

.multi-range-slider .bar-left {
  box-shadow: none;
}
.multi-range-slider .bar-right {
  box-shadow: none;
}
.multi-range-slider .bar-inner {
  box-shadow: none;
  background-color: var(--color-primary);
  border: none;
}

.multi-range-slider .bar {
}

.multi-range-slider .ruler {
  display: none;
}

.multi-range-slider {
  box-shadow: none;
  border: none;
}
</style>
