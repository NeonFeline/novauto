<script setup></script>

<template>
  <footer class="main_footer">
    <div class="main_footer_part contact">
      <img src="/logo.png" alt="" class="contact_logo" />
      <span class="contact_info">
        Novauto sp. z o.o. <br />

        ul. Radomska 67 <br />
        67-856 Pniewie
      </span>
    </div>
    <div class="main_footer_part info">
      <a href="#" class="info_link">Polityka prywatności</a>
      <a href="#" class="info_link">Ciasteczka cookies</a>
      <a href="#" class="info_link">RODO</a>
    </div>
    <div class="main_footer_part copyright">
      Novauto&copy; Wszystkie prawa zastrzeżone
    </div>
  </footer>
</template>

<style lang="scss">
@import "../assets/variables.scss";

.main_footer {
  background-color: var(--color-primary);
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 2.4rem 4.8rem;

  @media (width < $media-width-point-6) {
    flex-direction: column;
    gap: 3.6rem;
  }
}

.main_footer_part {
  flex: 0 0 1fr;
  width: 100%;
}

.contact {
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--color-white-1);
  font-size: 1.4rem;
  gap: 2.4rem;

  @media (width < $media-width-point-6) {
    flex-direction: column;
    gap: 1.2rem;
  }

  &_logo {
    height: 3.6rem;
    filter: brightness(0%) invert(100%);
  }

  &_info {
    font-weight: 700;
    text-align: center;
  }
}

.info {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.4rem;

  &_link {
    &:link,
    &:visited {
      color: var(--color-white-1);
      text-decoration: none;
      font-size: 1.4rem;
      border-bottom: solid 1px currentcolor;
    }

    &:hover,
    &:active {
      color: var(--color-primary-superdark);
    }
  }
}

.copyright {
  color: var(--color-white-1);
  font-size: 1.4rem;
  text-align: center;
}
</style>
