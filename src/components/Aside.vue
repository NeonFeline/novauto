<script setup>
import { ref, onMounted, computed } from "vue";
import MultiRangeSlider from "multi-range-slider-vue";
import RangeSlider from "./RangeSlider.vue";

const filterButton = ref(false);

// Filters
const filters = ref({
  kolor: { czerwony: true, niebieski: true, zolty: true, zielony: true },
  ilosc_dzwi: { 3: true, 5: true },
  naped: { benzyna: true, diesel: true, elektryk: true, hybryda: true },
});

function UpdateMinMileage(e) {
  console.log(e.value);
  mileageMin.value = +e.value;
}
function UpdateMaxMileage(e) {
  mileageMax.value = +e.value;
}

// false for every filter, because we initially want the filter list hidden
const generateFiltersInitialExpansion = function (filters) {
  const expansion = {};
  Object.keys(filters).forEach((key) => {
    expansion[key] = false;
  });

  expansion.przebieg = false;
  expansion.moc = false;
  expansion.rocznik = false;
  return expansion;
};

// Function to clear the filter selections
const clearFilterSelection = function (filter) {
  const selections = Object.keys(filters.value[filter]);

  // Find whether most of the filters are selected or not
  const mostSelected =
    selections.reduce((acc, key) => {
      if (filters.value[filter][key]) {
        acc++;
      }
      return acc;
    }, 0) >
    selections.length / 2;

  // Reverse the selection
  Object.keys(filters.value[filter]).forEach((key) => {
    filters.value[filter][key] = !mostSelected;
  });
};

// Whether filter is expanded or not
const filtersExpansions = ref(generateFiltersInitialExpansion(filters.value));
console.log(filtersExpansions.value);

// Lookup for filter true name
const filtersNameLookup = {
  kolor: "kolor",
  ilosc_dzwi: "ilość drzwi",
  naped: "napęd",
};

// Lookup for subfilter true name
const subfiltersNameLookup = {
  czerwony: "czerwony",
  niebieski: "niebieski",
  zolty: "żółty",
  zielony: "zielony",
  3: "3",
  5: "5",
  benzyna: "Benzyna",
  diesel: "Diesel",
  elektryk: "Elektryk",
  hybryda: "Hybryda",
};

const updatetest = function () {
  mileageMin.value = 50000;
};
</script>

<template>
  <aside :class="{ main_aside: true, 'main_aside--force': filterButton }">
    <button class="main_aside_show" @click="filterButton = !filterButton">
      <svg class="overview__icon-star">
        <use
          :xlink:href="`/icons.svg#icon-chevron-thin-${
            filterButton ? 'left' : 'right'
          }`"
        ></use>
      </svg>
    </button>
    <!-- Filters -->
    <div :class="{ filters: true, 'filters--force': filterButton }">
      <div class="aside_filter" v-for="filter in Object.keys(filters)">
        <div
          class="aside_filter_head"
          @click="filtersExpansions[filter] = !filtersExpansions[filter]"
        >
          <h3 class="aside_filter_name">
            {{ filtersNameLookup[filter] }}
          </h3>
          <button
            class="aside_filter_clear_btn"
            @click.stop=""
            @click="clearFilterSelection(filter)"
            v-show="filtersExpansions[filter]"
          >
            <svg class="overview__icon-star">
              <use xlink:href="/icons.svg#icon-cycle"></use>
            </svg>
          </button>
        </div>

        <ul class="filter_elements" v-show="filtersExpansions[filter]">
          <li
            v-for="subfilter in Object.keys(filters[filter])"
            @click="filters[filter][subfilter] = !filters[filter][subfilter]"
            :class="{
              filter_element: true,
              'filter_element--selected': filters[filter][subfilter],
            }"
          >
            {{ subfiltersNameLookup[subfilter] }}
          </li>
        </ul>
      </div>

      <!-- Mileage -->
      <div class="aside_slider">
        <div
          class="aside_slider_head"
          @click="filtersExpansions.przebieg = !filtersExpansions.przebieg"
        >
          <h3 class="aside_slider_name">
            Przebieg
          </h3>
        </div>
        <div class="aside_slider_box" v-show="filtersExpansions.przebieg">
          <RangeSlider min="0" max="2000000" step="10000" unit="km" />
        </div>
      </div>

      <!-- Power -->
      <div class="aside_slider">
        <div
          class="aside_slider_head"
          @click="filtersExpansions.moc = !filtersExpansions.moc"
        >
          <h3 class="aside_slider_name">
            Moc
          </h3>
        </div>
        <div class="aside_slider_box" v-show="filtersExpansions.moc">
          <RangeSlider min="0" max="2000" step="10" unit="KM" />
        </div>
      </div>

      <!-- Year -->
      <div class="aside_slider">
        <div
          class="aside_slider_head"
          @click="filtersExpansions.rocznik = !filtersExpansions.rocznik"
        >
          <h3 class="aside_slider_name">
            Rocznik
          </h3>
        </div>
        <div class="aside_slider_box" v-show="filtersExpansions.rocznik">
          <RangeSlider min="1950" max="2024" step="1" unit="" />
        </div>
      </div>
    </div>
  </aside>
</template>

<style lang="scss">
@import "../assets/variables.scss";

/////////////////
// Aside
.main_aside {
  flex: 0 0 23.52rem;
  background-color: var(--color-white-1);

  height: 100%;
  display: flex;
  flex-direction: column;
  gap: 1.6rem;
  margin-top: 1.2rem;

  @media (width < $media-width-point-4) {
    flex: 0 0 4.8rem;
  }

  &_show {
    background-color: var(--color-primary);
    margin-left: 2.4rem;
    margin-top: 2.4rem;
    border: none;
    border-radius: 1000px;
    width: 3.6rem;
    height: 3.6rem;
    justify-self: center;
    cursor: pointer;
    box-shadow: 0 0.5rem 0.5rem rgba(0, 0, 0, 0.1);
    display: flex;
    align-items: center;
    justify-content: center;

    @media (width > $media-width-point-4) {
      display: none;
    }

    svg {
      width: 2.2em;
      height: 2.2rem;
      color: var(--color-white-1);
      fill: currentcolor;
    }
  }

  &--force {
    flex: 0 0 100%;
  }
}

.filters {
  @media (width < $media-width-point-4) {
    display: none;
  }

  &--force {
    display: block;
  }
}

////////////////////////////
// Aside expandable filter
.aside_filter {
  &_name {
    font-weight: 300;
    text-transform: uppercase;

    font-size: 2rem;
    color: var(--color-primary-superdark);
  }

  &_head {
    display: flex;
    justify-content: space-between;
    box-shadow: var(--filter-shadow);
    z-index: 2;
    position: relative;
    padding: 1.2rem 2.4rem;
    cursor: pointer;
  }

  &_clear_btn {
    background-color: transparent;
    border: none;
    stroke: var(--color-primary-dark);
    fill: var(--color-primary-dark);
    cursor: pointer;
    transition: transform 0.2s;

    &:hover {
      transform: translateY(-2px);
    }

    &:active {
      transform: translateY(1px);
    }

    svg {
      width: 2rem;
      height: 2rem;
      stroke-width: 0.5px;
    }
  }
}

////////////////////////
// Aside min-max slider
.aside_slider {
  box-shadow: var(--filter-shadow);

  &_name {
    font-weight: 300;
    text-transform: uppercase;

    font-size: 2rem;
    color: var(--color-primary-superdark);
  }

  &_box {
    padding: 0rem 2.4rem 3.6rem 2.4rem;
  }

  &_head {
    padding: 1.2rem 2.4rem;
    cursor: pointer;
  }

  &_text {
    font-size: 1.6rem;
    display: flex;
    flex-direction: column;
    gap: 1.2rem;
    margin-top: 1.6rem;

    &--important {
      color: var(--color-primary-superdark);
      font-weight: 600;
    }

    &_input {
      border: none;
      -webkit-appearance: none;
      -moz-appearance: textfield;
      border-bottom: solid 2px var(--color-primary);
      transition: border 0.2s;
      font-size: 1.6rem;
      width: 100%;
      color: var(--color-dark-1);
      &:focus {
        border-bottom: solid 2px var(--color-secondary);
        outline: none;
      }
    }

    &_selection {
      display: flex;
      width: 100%;
      gap: 1.2rem;
    }
  }
}

.filter_elements {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 0.2rem;
  box-shadow: var(--filter-shadow);
}

.filter_element {
  padding: 1.2rem 2.4rem;
  background-color: var(--color-white-2);
  cursor: pointer;
  font-size: 1.2rem;
}

.filter_element--selected {
  background-color: var(--color-primary);
}
</style>
