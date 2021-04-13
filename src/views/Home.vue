<template>
    <ScrollToTopButton v-if="!isAtTop"  @click="scrollToElement('topPage')"/>
    <NavbarMobile v-if="(mobileMode && isAtTop) || (activatedNavbar && mobileMode)" @click="activatedNavbar = !activatedNavbar" />
    <header class="header">
    <nav id="nav">
      <div class="logo">
              <router-link class="logoName" to="/">
                  <img src="@/assets/logo.png" alt="">
              </router-link>
          </div>
      <ul>
        <li><router-link class="navLinks" to="/">127.0.0.1</router-link></li>
        <li><a @click="scrollToElement('lunch')">.lunch()</a></li>
        <li><a @click="scrollToElement('dinner')">.dinner()</a></li>
        <li><a @click="scrollToElement('snacks')">.snacks()</a></li>
      </ul>
      <div class="icons">
        <a href="https://en.wikipedia.org/wiki/Hummus" target="_blank"><i class="fab fa-wikipedia-w"></i></a>
        <a href="https://www.continente.pt/stores/continente/pt-pt/public/Pages/subcategory.aspx?cat=mercearia-tomate-feijao-grao-grao(eCsf_WebProductCatalog_MegastoreContinenteOnline_Continente_EUR_Colombo_PT)" target="_blank"><i class="fas fa-cart-plus"></i></a>
      </div>
	  </nav>
  </header>
    <div v-if="!activatedNavbar" id="topPage" class="pageContent">
      <section class="hero">
        <div class="heroContent">
          <h1>Hummussistant</h1>
          <p>Your personal assistant to fullfill your hummus needs, augmented with our special HummusAI.exe</p>
          <a class="elButton" @click="scrollToElement('lunch')">Execute hummus.exe</a>
        </div>
        <img class="heroImg" src="@/assets/Product/hero.svg" alt="">
      </section>
      <section id="lunch">
        
        <ul>
          <h1>.lunch()</h1>
          <a class="elButton" @click="getNextLunch()">Next Meal ➡️</a>
        </ul>
        <Food />
      </section>
      <Footer />
    </div>
  
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import NavbarMobile from '../components/NavbarMobile.vue';
import ScrollToTopButton from '../components/ScrollToTopButton.vue';
import Footer from '../components/Footer.vue';
import Food from '../components/Food.vue';
export default defineComponent({
  name: 'Home',
  data() {
    return {
      activatedNavbar: false,
      isAtTop: true,
      mobileMode: false,
      index: 0,
      meals: {
        lunch: [
          {id: 0, name: "Creamy Hummus Pasta", url: "https://youtu.be/KvJOZE15e3s?t=211", description: "", img: "hummusPasta.jpg"}
        ],
        dinner: [
          {id: 0, name: "King Oyster Mushrooms with tomate rice and hummus", url: "", description: "", img: "kingOyster.jpg"}
        ],
        snacks: [
          {id: 0, name: "Red Pepper Hummus", url: "https://youtu.be/yrR_7hlEGyw?t=143", description: "", img: "redHummus.jpg"},
          {id: 1, name: "Fresh Veggies with Hummus", url: "", description: "", img: "veggiesHummus.jpg"},
          {id: 2, name: "Bread with Hummus and tomate with oregano", url: "", description: "", img: "breadHummus.jpg"}
        ]

      }
    }
  },
  components: {
    NavbarMobile,
    ScrollToTopButton,
    Footer,
    Food,
  },
  created() {
    window.addEventListener('scroll', this.handleScroll);
    this.handleResize();
    window.addEventListener('resize', this.handleResize);
  },
  unmounted() {
    window.removeEventListener('scroll', this.handleScroll);
    window.removeEventListener('resize', this.handleResize);
  },
   methods: {
    getImgURL(image: String) {
        return require('../assets/' + image);
    },
    scrollToElement(destination: string) {
      const element = document.getElementById(destination);
      if (element) {
        element.scrollIntoView({behavior: 'smooth'});
      }
    },
    handleScroll () {
      window.pageYOffset >= 250 ? this.isAtTop = false : this.isAtTop = true;
    },
    handleResize () {
      this.mobileMode = window.innerWidth <= 1015;
      if(!this.mobileMode) {
        this.activatedNavbar = false;
      }
    },
    getNextLunch() {
      this.index += 1;

      if(this.index > 2) {
        this.index = 0;
      }
      return this.index;
    }
  },
});
</script>

<style lang="scss" scoped>
$buttonColorTest: #e96656;

.header {
  position: absolute;
	z-index: 10;
	width: 100%;
	opacity: 1;
	color: #fff;
	padding: 35px 100px 0;
  #nav {
    display: flex;
    justify-content: space-around;
    .logo {
      a {
        opacity: 1;
      }
      img {
        width: 90px;
        position: absolute;
        top: 15px;
        left: 40px;
      }
    }
    ul {
      display: flex;
      justify-content: center;
      list-style: none;
      li {
        padding: 10px;
        font-size: 26px;
        a {
            cursor: pointer;
            font-weight: bold;
            color: #000000;
            text-decoration: none;
        }  
      }
    }
    .icons {
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 26px;

      a {
        border-radius: 10px;
        padding: 10px;
        box-shadow: -2px -2px 3px rgba(255,255,255,0.05) , 2px 2px 3px rgba(0,0,0,0.2);
        transition: all 0.2s ease-out;

        &:hover {
          background-color: $buttonColorTest;
          color: white;
          transform: translateY(-2px);
        }
      }

      a:first-child {
        margin-right: 20px;
      }
    }
  }
}

.hero {
  height: 100vh;
}

section {
  height: 100vh;
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding: 0px 0px 0 50px;
  border: 1px solid red;
}

.heroContent {
  width: 40%;
  display: flex;
  justify-content: center;
  align-items: left;
  flex-direction: column;
  text-align: left;
    h1 {
      font-size: 48px;
      margin-bottom: 10px;
    }

    p {
      font-size: 20px;
      width: 80%;
    }

    a {
      max-width: 300px;
      position: relative;
      display: inline-block;
      text-align: center;
      text-transform: uppercase; 
      padding: 15px;
      margin: 30px 25px 0px 0px;
      font-size: 100% + 10%;
      font-weight: 600;
      border-radius: 5px;
      border: none;
      color: $buttonColorTest;
      background-color: white;
      transition: all 0.5s;

      &::before {
        position: absolute;
        content:"";
        border-radius: 5px;
        border-top: 5px solid lighten($buttonColorTest, 5%);
        border-left: 5px solid lighten($buttonColorTest, 5%);	
        border-right: 5px solid darken($buttonColorTest, 5%);
        border-bottom: 5px solid darken($buttonColorTest, 5%);
        top: 0px;
        right: 0px;
        bottom: 0px;
        left: 0px;	
        transition: 0.5s;
      }

      &:hover {
        box-shadow: 7px 7px darken($buttonColorTest, 10%), -7px -7px lighten($buttonColorTest, 10%);
        background-color: $buttonColorTest;
        color: #f7f7f7;
        cursor: pointer;
          &::before {
          border: 0px;
        }
      }
    }
  }

.heroImg {
  height: 800px;
  width: 60%;
}

.elButton {
  max-width: 300px;
      position: relative;
      display: inline-block;
      text-align: center;
      text-transform: uppercase; 
      padding: 15px;
      margin: 30px 25px 0px 0px;
      font-size: 100% + 10%;
      font-weight: 600;
      border-radius: 5px;
      border: none;
      color: $buttonColorTest;
      background-color: white;
      transition: all 0.5s;

      &::before {
        position: absolute;
        content:"";
        border-radius: 5px;
        border-top: 5px solid lighten($buttonColorTest, 5%);
        border-left: 5px solid lighten($buttonColorTest, 5%);	
        border-right: 5px solid darken($buttonColorTest, 5%);
        border-bottom: 5px solid darken($buttonColorTest, 5%);
        top: 0px;
        right: 0px;
        bottom: 0px;
        left: 0px;	
        transition: 0.5s;
      }

      &:hover {
        box-shadow: 7px 7px darken($buttonColorTest, 10%), -7px -7px lighten($buttonColorTest, 10%);
        background-color: $buttonColorTest;
        color: #f7f7f7;
        cursor: pointer;
          &::before {
          border: 0px;
        }
      }
    }

#lunch  {

    ul {
      height: 80%;
      border: 2px solid yellow;

      h1 {
        font-size: 48px;
      }
    }
  
}

</style>