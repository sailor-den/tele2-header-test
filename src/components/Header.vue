<template>
  <header>
    <div class="header__body">
      <div class="header__top">
        <div class="container">
          <div class="header__top-wrapper">
            <div class="header__logo">
              <a href="/" class="header__logo-link">
                <img src="../assets/logo.svg" class="img-responsive header__logo-img" alt="Tele2 logo">
              </a>
            </div>
            <div class="header__location">
              <button class="header__city-button">
                <img src="../assets/location.svg" class="img-responsive header__location-icon" alt="map pin">
                <span class="header__city">Москва и область</span>
              </button>
              <div class="notification-box__wrapper">
                <div class="notification-box">
                  <span class="notification-count"></span>
                  <div class="notification-bell">
                    <span class="bell-top"></span>
                    <span class="bell-middle"></span>
                    <span class="bell-bottom"></span>
                    <span class="bell-rad"></span>
                  </div>
                </div>
                <div @click="toggleMenu" class="menu-button"> 
                  <span :class="{ 'menu-open': isMenuOpen }">
                    <div class="burger">
                      <span></span>
                    </div>
                  </span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="header__bottom">
        <div class="container">
          <nav class="header__navigation">
            <ul class="header__submenu">
              <li
                v-for="(item, index) in submenuItems"
                :key="index"
                class="header__submenu-item"
                :class="{ 'header__submenu-item--active': activeIndex === index }"
                @click="setActiveMenuItem(index)"
              >
                <a href="#">{{ item }}</a>
              </li>
            </ul>
          </nav>
        </div>
        <div :class="['mobile-menu__wrapper', { 'mobile-menu__wrapper--active': isMenuOpen }]" >
          <div class="mobile-menu__top">
            <ul class="mobile-menu">
              <li
                v-for="(item, index) in submenuItems"
                :key="index"
                class="mobile-menu__item"
                :class="{ 'mobile-menu__item--active': activeIndex === index }"
                @click="setActiveMenuItem(index)"
              >
                <a href="#">{{ item }}</a>
              </li>
            </ul>
          </div>
          <div class="header__location header__location--mobile">
            <button class="header__city-button header__city-button--mobile">
              <img src="../assets/location.svg" class="img-responsive header__location-icon" alt="">
              <span class="header__city">Москва и область</span>
            </button>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>


<script setup>
  import { computed, ref, onMounted, onUnmounted } from 'vue';
  import { useMenuStore } from '../stores/useMenuStore';

  const menuStore = useMenuStore();
  const isMenuOpen = computed(() => menuStore.isMenuOpen);

  const submenuItems = [
    'Преимущества Tele2',
    'Тарифы',
    'Акции и спецпредложения',
    'Промотариф Tele2',
    'Технология eSIM',
    'Подключение нового абонента'
  ];

  const activeIndex = ref(0);

  const setActiveMenuItem = (index) => {
    activeIndex.value = index; 
  };

  const toggleMenu = () => {
    menuStore.toggleMenu();
  };

  const checkScreenWidth = () => {
    if (window.innerWidth > 910 && isMenuOpen.value) {
      menuStore.toggleMenu(); 
    }
  };

  onMounted(() => {
    window.addEventListener('resize', checkScreenWidth);
  });

  onUnmounted(() => {
    window.removeEventListener('resize', checkScreenWidth);
  });
</script>


<style scoped>

.container {
  max-width: 1116px;
  margin: auto;
}

.img-responsive {
  display: block;
  height: auto;
  max-width: 100%;
}

.header__top {
  background-color:  #1F2229;
  padding: 8px 0 5px;
}

.header__logo-link {
  display: inline-block;
}

.header__top-wrapper {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.header__city-button {
  display: flex;
  align-items: center;
  background-color: transparent;
  border: none;
  gap: 8px;
  padding: 0;
  cursor: pointer;
}

.header__city {
  font-size: 14px;
  font-weight: 400;
  line-height: 18px;
  color: #7C8792;
}

.header__location {
  display: flex;
  gap: 35px;
  align-items: center;
}

.header__bottom {
  background-color: #fff;
}

.header__navigation {
  padding: 15px 0 0 0;
  border-bottom: 2px solid #D3D9DF;
}

.header__submenu {
  display: flex;
  align-items: center;
  gap: 18px;
  width: 100%;
  padding: 0;
  margin: 0;
}

.header__submenu-item {
  list-style-type: none;
  position: relative;
  font-size: 14px;
  font-weight: 400;
  line-height: 18px;
  padding-bottom: 12px;
}

.header__submenu-item a {
  text-decoration: none;
  color: #7C8792;
}

.header__submenu-item--active::after {
  content: '';
  width: 100%;
  height: 2px;
  background-color: #1F2229;
  position: absolute;
  bottom: -2px;
  left: 0;
}

.header__submenu-item--active a {
  color: #1F2229;
  font-weight: bold;
}

.menu-button {
  display: none;
}

.mobile-menu__wrapper {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 20;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: calc(100% - 45px);
  margin-top: 45px;
  background-color: #fff;
  opacity: 0;
  transform: translateY(-5px); 
  transition: opacity 0.3s ease, transform 0.3s ease; 
  visibility: hidden;
}

.mobile-menu__wrapper--active {
  opacity: 1; 
  transform: translateY(0); 
  visibility: visible;
}

.header__bottom--mobile {
  background-color:  #1F2229;
  padding: 8px 10px;
}

.header__location--mobile {
  background-color:  #F3F5F6;
}

.burger {
  border-radius: 4px;
  height: 40px;
  position: relative;
  width: 30px;
  z-index: 10;
  top: 20px;
}

.burger span, .burger span:after, .burger span:before {
  background-color: #fff;
  display: block;
  height: 3px;
  outline: 1px solid transparent;
  transition-duration: .3s;
  transition-property: background-color, transform;
  width: 30px;
  border-radius: 8px;
}

.burger span:after, .burger span:before {
  content: "";
  position: absolute;
}

.burger span:before {
  top: -13px;
}

.burger span:after {
  top: 13px;
}

.menu-open .burger span {
  background-color: transparent;
}

.burger span::before {
    top: -9px;
}

.menu-open .burger span::before {
  transform: translateY(9px) rotate(45deg);
}

.menu-open .burger span:before, .menu-open .burger span:after {
  background-color: #ffffff;
}

.burger span::after {
  top: 9px;
}

.menu-open .burger span::after {
  transform: translateY(-9px) rotate(-45deg);
}

.notification-box__wrapper {
  display: flex;
  gap: 26px;
}

.notification-box {
  position: relative;
  z-index: 99;
  top: 0px;
  width: 19px;
  height: 19px;
  text-align: center;
  transform: rotate(-30deg);
}

.notification-count {
  position: absolute;
  z-index: 1;
  top: 5px;
  right: 1px;
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background-color:  #3FCBFF;
  color: #fff;
  animation: zoom 3s 3s both infinite;
}

.notification-bell {
  animation: bell 1s 1s both infinite;
}

.notification-bell * {
  display: block;
  margin: 0 auto;
  background-color: #fff;
  box-shadow: 0px 0px 15px #fff;
}

.bell-top {
  width: 4px;
  height: 4px;
  border-radius: 3px 3px 0 0;
}

.bell-middle {
  width: 12px;
  height: 12px;
  margin-top: -1px;
  border-radius: 12.5px 12.5px 0 0;
}

.bell-bottom {
  position: relative;
  z-index: 0;
  width: 16px;
  height: 2px;
  top: -1px;
}

.bell-bottom::before, .bell-bottom::after {
  content: '';
  position: absolute;
  top: -4px;
}

.bell-bottom::before {
  left: 1px;
  border-bottom: 4px solid #fff;
  border-right: 0 solid transparent;
  border-left: 4px solid transparent;
}

.bell-bottom::after {
  right: 1px;
  border-bottom: 4px solid #fff;
  border-right: 4px solid transparent;
  border-left: 0 solid transparent;
}

.bell-rad {
  width: 6px;
  height: 4px;
  margin-top: -1px;
  border-radius: 0 0 4px 4px;
  -webkit-animation: rad 1s 2s both infinite;
  animation: rad 1s 2s both infinite;
}

 @keyframes rad {
  0% {
      transform: translateX(0);
  }
  10% {
      transform: translateX(3px);
  }
  20% {
      transform: translateX(0);
  }
  80% {
      transform: translateX(0);
  }
  90% {
      transform: translateX(-3px);
  }
  100% {
      transform: translateX(0);
  }
}

@keyframes bell {
  0% {
      transform: rotate(0);
  }
  10% {
      transform: rotate(30deg);
  }
  20% {
      transform: rotate(0);
  }
  80% {
      transform: rotate(0);
  }
  90% {
      transform: rotate(-30deg);
  }
  100% {
      transform: rotate(0);
  }
}

@keyframes zoom {
  0% {
    opacity: 0;
      transform: scale(0);
  }
  10% {
      opacity: 1;
      transform: scale(1);
  }
  50% {
      opacity: 1;
  }
  51% {
      opacity: 0;
  }
  100% {
      opacity: 0;
  }
} 

.desktop-nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #222;
  padding: 1rem;
}

.desktop-menu {
  display: flex;
  gap: 2rem;
  list-style: none;
}

.region {
  color: #888;
}

.mobile-nav {
  display: none;
}

.menu-button {
  background: none;
  border: none;
}

.mobile-menu {
  list-style: none;
  padding: 0 15px;
  display: flex;
  flex-direction: column;
  gap: 16px;
  margin: 24px 0 0 0;
}

.mobile-menu__item {
  border-bottom: 1px solid #EDEDED;
  padding-bottom: 7px;
}

.mobile-menu__item a {
  text-decoration: none;
  font-size: 16px;
  font-weight: 700;
  line-height: 22px;
  color: #959597;
}


@media (max-width: 1200px) {
  .container {
    padding: 0 10px;
  }
}

@media (max-width: 910px) {
  .container {
    padding: 0 18px;
  }

  .header__logo {
    max-width: 48px;
  }

  .header__navigation {
    display: none;
  }

  .menu-button {
    display: block;
  }

  .notification-box {
    top: 4px;
    left: 14px;
  }

  .burger {
    height: 32px;
    top: 13px;
    left: 13px;
  }

  .burger span, .burger span:after, .burger span:before {
    width: 18px;
  }

  .burger span::before {
    top: -7px;
  }

  .burger span::after {
    top: 7px;
  }

  .menu-open .burger span::before {
    transform: translateY(7px) rotate(45deg);
  } 

  .menu-open .burger span::after {
    transform: translateY(-7px) rotate(-45deg);
  }

  .header__city-button {
    display: none;
  }

  .header__city-button--mobile {
    display: flex;
    padding: 16px 15px;
  }
}

@media (max-width: 768px) {
  .desktop-nav {
    display: none;
  }

  .mobile-nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #222;
    padding: 1rem;
  }
}
</style>
