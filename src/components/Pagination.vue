<script setup>
import { ref, onMounted, computed } from "vue";

const pages = ref([-1, -1, 1, 2, 3]);
const selected = 1;
</script>

<template>
  <div class="pagination">
    <button class="page_number page_btn">
      <svg class="overview__icon-star">
        <use xlink:href="/icons.svg#icon-chevron-thin-left"></use>
      </svg>
    </button>
    <button
      :class="{
        page_number: true,
        'page_number--selected': page == selected,
        'page_number--none': page == -1,
      }"
      v-for="page in pages"
    >
      {{ page }}
    </button>
    <button class="page_number page_btn">
      <svg class="overview__icon-star">
        <use xlink:href="/icons.svg#icon-chevron-thin-right"></use>
      </svg>
    </button>
  </div>
</template>

<style lang="scss">
.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 2.4rem;
  margin-bottom: 2.4rem;
  margin-top: 1.2rem;
}

.page {
  &_number {
    border-radius: 100px;
    width: 4.2rem;
    height: 4.2rem;
    display: flex;
    align-items: center;
    justify-content: center;
    border: solid 1px var(--color-primary);
    color: var(--color-primary-superdark);
    font-size: 1.6rem;
    cursor: pointer;
    background-color: transparent;
    transition: transform 0.2s;

    &--selected {
      background-color: var(--color-primary);
      color: var(--color-white-1);
    }

    &:hover {
      transform: translateY(-3px);
    }

    &:active {
      transform: translateY(1px);
    }

    &--none {
      opacity: 0;
      cursor: auto;
    }
  }

  &_btn {
    width: 3.6rem;
    height: 3.6rem;
    border: none;
    svg {
      width: 1.4rem;
      height: 1.4rem;
      color: var(--color-primary-superdark);
      stroke: currentColor;
      fill: currentColor;

      stroke-width: 0.5px;
    }
  }
}
</style>
