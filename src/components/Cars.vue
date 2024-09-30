<script setup>
import { ref, onMounted, computed } from "vue";
import Pagination from "./Pagination.vue";

const fuelTypes = ["Benzyna", "Diesel", "Elektryk", "Hybryda"];
const cars = ref([
  {
    src: "/cars/1.jpg",
    name: "Toyota korolla",
    mileage: 112000,
    fuel: fuelTypes[1],
    year: 2014,
    power: 213,
    price: 42200,
  },
  {
    src: "/cars/2.jpg",
    name: "Ford Mustang",
    mileage: 1000,
    fuel: fuelTypes[0],
    year: 2015,
    power: 516,
    price: 340000,
  },
  {
    src: "/cars/3.webp",
    name: "Chevrolet Corvetta",
    mileage: 10000,
    fuel: fuelTypes[0],
    year: 2004,
    power: 718,
    price: 520000,
  },
  {
    src: "/cars/4.webp",
    name: "Lamborgini",
    mileage: 50000,
    fuel: fuelTypes[0],
    year: 2014,
    power: 617,
    price: 760000,
  },
  {
    src: "/cars/5.jpg",
    name: "Kia",
    mileage: 73000,
    fuel: fuelTypes[3],
    year: 2017,
    power: 813,
    price: 65000,
  },
  {
    src: "/cars/6.webp",
    name: "Merccedes",
    mileage: 23000,
    fuel: fuelTypes[3],
    year: 2014,
    power: 652,
    price: 120000,
  },
  {
    src: "/cars/7.jpg",
    name: "Merccedes",
    mileage: 85000,
    fuel: fuelTypes[2],
    year: 2012,
    power: 734,
    price: 63000,
  },
  {
    src: "/cars/8.jpg",
    name: "Merccedes",
    mileage: 100000,
    fuel: fuelTypes[0],
    year: 2011,
    power: 957,
    price: 34000,
  },
  {
    src: "/cars/9.jpg",
    name: "Porche",
    mileage: 50000,
    fuel: fuelTypes[2],
    year: 2008,
    power: 514,
    price: 86000,
  },
  {
    src: "/cars/10.webp",
    name: "Porche",
    mileage: 20000,
    fuel: fuelTypes[0],
    year: 2004,
    power: 642,
    price: 122000,
  },
  {
    src: "/cars/11.avif",
    name: "Macklaren",
    mileage: 23000,
    fuel: fuelTypes[0],
    year: 2021,
    power: 624,
    price: 123000,
  },
  {
    src: "/cars/12.webp",
    name: "Macklaren",
    mileage: 150000,
    fuel: fuelTypes[0],
    year: 2014,
    power: 1421,
    price: 1740000,
  },
  {
    src: "/cars/13.jpg",
    name: "Dodge",
    mileage: 250000,
    fuel: fuelTypes[1],
    year: 2016,
    power: 231,
    price: 12300,
  },
  {
    src: "/cars/14.webp",
    name: "Ford",
    mileage: 230000,
    fuel: fuelTypes[1],
    year: 2017,
    power: 224,
    price: 11000,
  },
  {
    src: "/cars/15.webp",
    name: "Ford",
    mileage: 1450000,
    fuel: fuelTypes[1],
    year: 2012,
    power: 112,
    price: 8000,
  },
  {
    src: "/cars/16.webp",
    name: "Ford",
    mileage: 520000,
    fuel: fuelTypes[1],
    year: 2014,
    power: 134,
    price: 9000,
  },
  {
    src: "/cars/17.jpg",
    name: "Fiat 126p",
    mileage: 1730000,
    fuel: fuelTypes[1],
    year: 1991,
    power: 64,
    price: 22000,
  },
  {
    src: "/cars/18.jpg",
    name: "Fiat 126p",
    mileage: 1620000,
    fuel: fuelTypes[1],
    year: 1990,
    power: 44,
    price: 26000,
  },
]);
</script>

<template>
  <div class="main_content">
    <div class="main_grid">
      <div class="car_info" v-for="car in cars">
        <div class="car_info_imgbox">
          <img :src="car.src" alt="" class="car_info_img" />
        </div>
        <div class="car_info_stats">
          <span class="car_info_name">{{ car.name }}</span>

          <div class="car_info_stat">
            <span class="car_info_stat__name">Napęd</span>
            <span class="car_info_stat__value">{{ car.fuel }}</span>
          </div>

          <div class="car_info_stat">
            <span class="car_info_stat__name">Przebieg</span>
            <span class="car_info_stat__value">{{ car.mileage }} km</span>
          </div>

          <div class="car_info_stat">
            <span class="car_info_stat__name">Moc</span>
            <span class="car_info_stat__value">{{ car.power }} KM</span>
          </div>

          <div class="car_info_stat">
            <span class="car_info_stat__name">Rocznik</span>
            <span class="car_info_stat__value">{{ car.year }}</span>
          </div>
        </div>
        <div class="car_info_price">{{ car.price }} zł</div>
      </div>
    </div>
    <Pagination />
  </div>
</template>

<style lang="scss">
@import "../assets/variables.scss";

.main_content {
  width: 100%;
}

/////////////////////////
// Main grid
.main_grid {
  width: 100%;
  padding: 2.4rem;

  display: grid;
  grid-template-columns: repeat(6, 1fr);
  justify-content: space-between;
  gap: 2rem;

  @media (width < $media-width-point-1) {
    grid-template-columns: repeat(5, 1fr);
  }
  @media (width < $media-width-point-2) {
    grid-template-columns: repeat(4, 1fr);
  }
  @media (width < $media-width-point-3) {
    grid-template-columns: repeat(3, 1fr);
  }
  @media (width < $media-width-point-5) {
    grid-template-columns: repeat(2, 1fr);
  }
  @media (width < $media-width-point-6) {
    grid-template-columns: repeat(1, 1fr);
  }
}

/////////////////////////
// Car information card
.car_info {
  height: 42rem;
  padding: 1.2rem 1.2rem;

  border-radius: var(--default-border-radius);

  box-shadow: 0 0.5rem 0.5rem rgba(0, 0, 0, 0.1);
  transition: all 0.2s;

  cursor: pointer;
  display: flex;
  flex-direction: column;
  justify-content: space-between;

  @media (width < $media-width-point-5) {
    height: 46rem;
  }
  @media (width < $media-width-point-6) {
    height: 66rem;
  }

  &_imgbox {
    flex: 0 0 13rem;

    position: relative;
    overflow: hidden;

    border-radius: var(--default-border-radius);

    @media (width < $media-width-point-5) {
      flex: 0 0 16rem;
    }

    @media (width < $media-width-point-6) {
      flex: 0 0 36rem;
    }
  }

  &_img {
    display: block;

    width: 100%;

    position: absolute;
    top: 50%;
    left: 0;

    transition: all 0.2s;
    transform: translateY(-50%);
  }

  &_stats {
    display: flex;
    flex-direction: column;

    gap: 0.4rem;
    height: 100%;
  }

  &_stat {
    display: flex;
    justify-content: space-between;
    padding: 0.6rem 1.2rem;
    font-size: 1.2rem;
    border-radius: 2px;

    &:hover {
      background-color: var(--color-white-light);
    }

    &__name {
    }

    &__value {
      color: var(--color-primary-superdark);
    }
  }

  &_name {
    margin-top: 0.8rem;
    margin-bottom: 0.8rem;
    padding: 0.6rem 1.2rem;

    font-size: 2rem;
  }

  &_price {
    font-size: 2.4rem;
    font-weight: 500;
    color: var(--color-primary);
    background-color: var(--color-white-1);
    text-align: center;
    padding: 1.2rem 2.4rem;
    margin-top: 1.2rem;
    border-radius: var(--default-border-radius);
    border: solid 2px var(--color-primary);
    transition: background-color 0.2s, color 0.2s;
  }

  &:hover {
    box-shadow: 0 1rem 2rem rgba(0, 0, 0, 0.1);
    transform: translateY(-3px);

    .car_info_price {
      background-color: var(--color-primary);
      color: var(--color-white-1);
    }
  }
}
</style>
