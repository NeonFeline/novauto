<script setup></script>

<template>
  <header class="main_nav">
    <img src="/logo.png" alt="" class="nav_logo" />
    <div class="nav_search">
      <input
        type="text"
        class="nav_search_input"
        placeholder="Wyszukaj spośród ponad 20 tysięcy samochodów"
      />
      <button class="nav_search_btn">
        <svg class="overview__icon-star">
          <use xlink:href="/icons.svg#icon-magnifying-glass"></use>
        </svg>
      </button>
    </div>
    <button class="nav_btn">
      <svg class="overview__icon-star">
        <use xlink:href="/icons.svg#icon-chat"></use>
      </svg>
      <span class="nav_btn_number">
        7
      </span>
    </button>
    <button class="nav_btn">
      <svg class="overview__icon-star">
        <use xlink:href="/icons.svg#icon-home"></use>
      </svg>
    </button>
  </header>
</template>

<style lang="scss">
@import "../assets/variables.scss";

/////////////////////
// Navigation
.main_nav {
  display: flex;
  justify-content: space-between;
  align-items: center;

  height: 9.2rem;

  box-shadow: 0 1rem 1rem rgba(0, 0, 0, 0.05);
  z-index: 1;

  @media (width < $media-width-point-4) {
    flex-wrap: wrap;
    height: 18rem;
  }
}

/////////////////////
// Logo
.nav_logo {
  height: 3.6rem;
  padding: 2.4rem 4.8rem;

  box-sizing: content-box;

  @media (width < $media-width-point-4) {
    margin-right: auto;
  }
}

/////////////////////
// Searchbar
.nav_search {
  @media (width < $media-width-point-4) {
    width: 90%;
    order: 1;
  }

  display: flex;

  width: 50%;
  margin-left: auto;
  margin-right: auto;

  border-radius: 1000px;

  box-shadow: 0 1rem 1rem rgba(0, 0, 0, 0.05);
  transition: width 0.2s;

  /////////////////////
  // Input
  &_input {
    width: 100%;
    padding: 1.2rem 2.4rem;

    border: none;
    border-radius: 100px;

    font-size: 1.6rem;

    color: var(--color-dark-1);

    &:focus {
      outline: none;
    }

    &::placeholder {
      color: var(--color-white-3);
    }
  }

  /////////////////////
  // Search button
  &_btn {
    width: 8.4rem;
    margin-left: -1.4rem;

    border-top-right-radius: 100px;
    border-bottom-right-radius: 100px;
    border: none;

    background-color: var(--color-primary);

    cursor: pointer;

    &:hover {
      background-color: var(--color-primary-dark);
    }

    svg {
      width: 2.6rem;
      height: 2.6rem;

      color: var(--color-white-1);
      fill: currentColor;
    }
  }
}

// Widen the search bar when selected
.nav_search:has(.nav_search_input:focus) {
  width: 60%;
  @media (width < $media-width-point-4) {
    width: 90%;
  }
}

////////////////////////
// Navigation buttons
.nav_btn {
  align-self: stretch;
  border: none;
  background-color: transparent;
  padding: 1.2rem 2.4rem;

  border-left: solid 1px var(--color-primary);
  position: relative;
  cursor: pointer;

  color: var(--color-dark-1);
  font-weight: 500;
  font-size: 1.6rem;

  ////////////////////////
  // Icon
  svg {
    width: 2.6rem;
    height: 2.6rem;

    color: var(--color-dark-1);
    stroke: currentColor;
    fill: currentColor;

    transition: all 0.2s;
  }

  ////////////////////////
  // Number near the icon
  &_number {
    width: 1.6rem;
    height: 1.6rem;

    display: flex;
    align-items: center;
    justify-content: center;

    position: absolute;
    top: 2rem;
    right: 1.5rem;

    background-color: var(--color-primary);
    font-size: 1rem;

    border-radius: 1000px;
    transition: all 0.2s;
  }

  ////////////////////////
  // Cool color animation
  &::after {
    content: "";
    display: block;
    width: 100%;
    height: 100%;

    position: absolute;
    top: 0;
    left: 0;
    z-index: -1;

    background-color: var(--color-primary);
    transform: translateY(-100%);
    transition: 0.2s;
  }

  // Change the icon color when hovered
  &:hover {
    svg {
      color: var(--color-white-1);
    }

    .nav_btn_number {
      background-color: var(--color-white-1);
      color: var(--color-primary);
    }
  }
}

// Slide the color block in when hovered
.nav_btn:hover::after {
  transform: translateY(0%);
}
</style>
