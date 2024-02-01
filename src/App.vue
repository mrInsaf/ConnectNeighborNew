<template >
    <header>
        <div class="logo">
            <img src="./icon.png" alt="">
            <h2>ConnectNeighbour</h2>
        </div>
        <div class="desktop-menu">
            <ul>
                <li>Главная</li>
                <li>Профиль</li>
                <li>О нас</li>
                <li>Понравившееся</li>
                <li>Зарегистрироваться</li>
                <li>Войти</li>
            </ul>
        </div>
        <div class="mobile-menu" @click="openMenu">
          <img src="./Menu.png" alt="">
        </div>

    </header>
  <div class="mobile-menu" v-if="windowWidth <= 930">
    <ul v-if="menuIsOpen">
      <li>Главная</li>
      <li>Профиль</li>
      <li>О нас</li>
      <li>Понравившееся</li>
      <li>Зарегистрироваться</li>
      <li>Войти</li>
    </ul>
  </div>


    <div class="main" >
        <div class="container">
            <img :src="imgList[2]">
            <div class="overlay">
                <h1>Найди соседа для совместного проживания</h1>
            </div>
        </div>

        <div class="tutorial-container">
            <div class="tutorial">
                <img src="./filter.png" alt="">
                <p>Подбери фильтры для жилья</p>
            </div>
            <div class="tutorial">
                <img src="./perfect-house.png" alt="">
                <p>Найди идеальное жилье</p>
            </div>
            <div class="tutorial">
                <img src="./liked-house.png" alt="">
                <p>Отметь его лайком</p>
            </div>
            <div class="tutorial">
                <img src="./people-list.png" alt="">
                <p>Просмотри список также лайкнувших это жилье людей</p>
            </div>
        </div>

        <div class="filter-container">
            <h3>Критерии жилья</h3>
            <div class="filters">
                <div class="filter">
                    <label for="room-num">Количество комнат</label>
                    <select id="room-num">
                        <option value="1">1</option>
                        <option value="2">2</option>
                        <option value="3">3</option>
                        <option value="4">4</option>
                    </select>
                </div>

                <div class="filter">
                    <label for="region">Район</label>
                    <input type="text" id="region">
                </div>
                
                <div class="filter">
                    <label for="price">Цена</label>
<!--                    <div class="price-filters">-->
                        <input type="number" placeholder="От">
<!--                    </div>-->
                </div>

                <div class="filter">
                  <label for="price" style="color: white">Цена</label>
                  <input type="number" placeholder="До">
                </div>
                <button>
                    Найти
                </button>
            </div>
        </div>

      <div class="daily-offer-container">
        <div class="daily-offer">
          <h2>Предложение дня</h2>
          <div class="arrow left-arrow" @click="moveLeft">
              <img src="./arrow_left.png" alt="yoo">
          </div>
          <div
              class="card"
              v-for="(housing, idx) in visibleHousings"
              v-bind:key="housing.id"
          >
            <product-card
                :housing="housing"
                :idx="idx"
            ></product-card>
          </div>
          <div class="arrow right-arrow" @click="moveRight">
              <img src="./arrow_right.png" alt="yoo">
          </div>
        </div>
      </div>


    </div>

    <footer>
        © Copyright Insaf Salakhov {{windowWidth}}
    </footer>

</template>

<script>
import ProductCard from './components/ProductCard.vue';

    export default{
      name: "App",
      components: {
        ProductCard,
      },

        data() {
            return {
              menuIsOpen: false,
              windowWidth: window.innerWidth,
                imgList: [
                    "https://mykaleidoscope.ru/uploads/posts/2021-03/1616683945_1-p-bolshie-kvartiri-studii-1.jpg",
                    "https://pro-dachnikov.com/uploads/posts/2021-10/1633374614_44-p-krasivie-kukhni-gostinie-intereri-v-domakh-44.jpg",
                    "https://mebel-complect.ru/wp-content/uploads/a/7/5/a7580da977a7ca44f26de12b3e3d7087.jpeg",
                ],
              housingList: [
                {
                  id: 1,
                  imageSrc: "https://cdn-p.cian.site/images/2078187335-4.jpg",
                  name: "1-комн. апартаменты, 39,7 м²",
                  price: "7 020 000",
                },
                {
                  id: 2,
                  imageSrc: "https://cdn-p.cian.site/images/2060591960-4.jpg",
                  name: "1-комн. квартира, 41,6 м²",
                  price: "10 600 000",
                },

                {
                  id: 3,
                  imageSrc: "https://cdn-p.cian.site/images/2043000784-4.jpg",
                  name: "2-комн. квартира, 64 м²",
                  price: "18 890 000",
                },

                {
                  id: 4,
                  imageSrc: "https://cdn-p.cian.site/images/kvartira-sosenskoe-velaskesa-bulvar-2090223548-4.jpg",
                  name: "Товар 2",
                  price: "7 700 000",
                },

              ],
              currentIndex: 0,
            }
        },
      computed: {
          visibleHousings() {
              let numOfCards = 0;
              if (this.windowWidth > 1222) numOfCards = 3
            else if (this.windowWidth > 820) numOfCards = 2
            else numOfCards = 1

              return this.housingList.slice(0, numOfCards)
          },

          indexList() {
              let idxList = []
              for (let i = 0; i < this.housingList.length; i++) {
                  idxList.push(i);
              }
              return idxList
          },

          totalCards() {
              return this.housingList.length
          }
      },

      methods: {
        moveLeft() {
          let lastIdx = this.housingList.pop()
          this.housingList.unshift((lastIdx))
        },

        moveRight() {
          let firstIndx = this.housingList.shift()
          this.housingList.push(firstIndx)
        },

        openMenu() {
            this.menuIsOpen = !this.menuIsOpen
        }
      },

      mounted() {
        window.onresize = () => {
          this.windowWidth = window.innerWidth
        }
      }
    }
</script>

<style>
    body {
        margin: 0;
        padding: 0;
        font-family: Arial, sans-serif;
    }

    header {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        background-color: #fbffc9;
        color: #000000;
        //padding: 10px;
    }
    
    header .logo {
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
    }

    header .logo img {
      max-height: 40px;
      padding-right: 20px;
    }

    header .mobile-menu {
      display: none;
    }

    header .mobile-menu img {
      width: 30px;
      padding-right: 20px;
    }

    header .desktop-menu ul {
        display: flex;
        flex-direction: row;
        list-style: none;
    }

    header .mobile-menu ul {
      position: relative;
      display: flex;
      flex-direction: column;
      list-style: none;
    }

    header ul li {
        padding: 10px;
    }

    .mobile-menu ul {
      text-align: center;
      list-style: none;
      padding: 10px;
    }

    .mobile-menu ul li {
      padding: 10px
    }

    .main {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
        
    .container {
        position: relative;
        width: 100%;
        max-height: 100%;
    }

    .container img {
        width: 100%;
        height: 600px;
        filter: brightness(20%);
        object-fit:cover;
    }

    .overlay {
        /* border: 2px solid rgb(0, 0, 0); */
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        position: absolute;
        top: 10px;
        width: 100%;
        height: 100%;
    }

    .overlay h1 {
        align-self: flex-start;
        max-width: 80%;
        color: #ffffff;
        font-size: 90px;
        padding: 10px;
    }

    .tutorial-container {
        /* border: 2px solid rgb(0, 0, 0);  */
        background-color: #fbffc9;
        padding-top: 20px;
        padding-bottom: 20px;
        display: flex;
        width: 100%;
        flex-direction: row;
        justify-content: space-around;
    }

    .tutorial-container .tutorial {
        max-width: 300px;
        /* border: 2px solid rgb(110, 110, 110);  */
        display: flex;
        flex-direction: row;
        align-items: center;
    }

    .tutorial-container .tutorial > * {
        //padding: 10px
    }

    .tutorial-container .tutorial img {
        max-width: 50px;
        max-height: 50px;
    }

    .filter-container {
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;
      grid-template-rows: 1fr 1fr;
      grid-column-gap: 10px;
      //border: 1px solid green;
      width: 60%;
      padding-bottom: 100px;

    }

    .filter-container h3 {
      align-self: center;
      //border: 1px solid green;
      grid-column-start: 1;
      grid-column-end: 4;
    }

    .filter-container .filters {
      height: 100%;
      grid-column-start: 1;
      grid-column-end: 4;
        //flex-shrink: 1;
        flex-grow: 1;
        display: grid;
        grid-template-columns: 1fr 1fr 1fr 1fr;
      grid-column-gap: 10px;
      grid-row-gap: 10px;
      justify-content: center;
        //border: 1px solid black;
        align-items: center;
    }

    .filter-container .filters .filter {
        display: flex;
        flex-direction: column;
      text-align: center;
    }

    label {
        margin-bottom: 10px;
    }

    .filter-container .filters .filter select{
        height: 40px;
      border: 1px solid #d5d5d5;
      border-radius: 10px;
        //width: 200px;
    }

    .filter-container .filters .filter input {
      border: 1px solid #d5d5d5;
        height: 40px;
      border-radius: 10px;
        //width: 200px
    }

    .filter-container .filters button {
      grid-column-start: 4;
      background: #f2bdf6;
      height: 40px;
      border: 0;
      border-radius: 10px;
    }

    .daily-offer-container {
      width: 100%;
      display: flex;
      flex-direction: column;
      align-items: center;
      background-color: #fbffc9;
    }

    .daily-offer {
      position: relative;
      width: 70%;
      //border: 1px solid black;
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;
      justify-self: center;
    }

    .daily-offer h2 {
      //border: 1px solid black;
      grid-column-start: 1;
      grid-column-end: 2;
    }

    .daily-offer .card {
      grid-row-start: 2;
      //border: 1px solid black;
      //justify-self: center;
    }

    .arrow img {
      width: 40px;
      position: absolute;
      top: 50%;
    }

    .left-arrow img{
      left: -50px;
    }

    .right-arrow img{
      right: -50px;
    }

    footer {
        text-align: center;
        background-color: #fbffc9;
    }

    @media (max-width: 1170px) {
      .filter-container .filters {
        grid-template-columns: 1fr 1fr;
      }
    }
    
    @media (max-width: 930px) {
      header .desktop-menu ul {
        display: none;
      }

      header .mobile-menu {
        display: flex;
        flex-direction: column;
        align-items: center;
      }

      .tutorial-container {
        flex-direction: column;
        align-items: center;
      }
      .tutorial-container .tutorial {
        padding-bottom: 24px;
      }

    ;
    }

    @media (max-width: 660px) {
      .filter-container {
        display: flex;
        flex-direction: column;
        //border: 1px solid black;
      }

      .filter-container .filters {
        display: flex;
        flex-direction: column;
        //border: 1px solid black;
      }

      .main .overlay h1 {
        font-size: 70px;
      }

    }
</style>
