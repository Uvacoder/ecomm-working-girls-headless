<template>
  <div>
    <Header />
    <Slider />
    <CollectionBanner />
    <ProductSlider :products="products" @openQuickview="showQuickview" @openCompare="showCoampre" @openCart="showCart" />
    <Banner />
    <CountDown />
    <ProductTab :products="products" :category="category" @openQuickview="showQuickview" @openCompare="showCoampre" @openCart="showCart" />
    <Services />
    <LogoSlider />
    <Footer />
    <quickviewModel :openModal="showquickviewmodel" :productData="quickviewproduct" />
    <compareModel :openCompare="showcomparemodal" :productData="comapreproduct" @closeCompare="closeCompareModal" />
    <cartModel :openCart="showcartmodal" :productData="cartproduct" @closeCart="closeCartModal" :products="products" />
    <newsletterModel />
  </div>
</template>
<script>
import { mapState } from 'vuex'
import Header from '../../../components/header/header1'
import Footer from '../../../components/footer/footer1'
import quickviewModel from '../../../components/widgets/quickview'
import compareModel from '../../../components/widgets/compare-popup'
import cartModel from '../../../components/cart-model/cart-modal-popup'
import newsletterModel from '../../../components/widgets/newsletter-popup'
import Slider from './components/slider'
import CollectionBanner from './components/collection_banner'
import ProductSlider from './components/product_slider'
import Banner from './components/banner'
import ProductTab from './components/product_tab'
import Services from './components/services'
import Blog from './components/blog'
import Instagram from './components/instagram'
import LogoSlider from './components/logo_slider'
import CountDown from './components/countdown';

export default {
  components: {
    Header,
    Slider,
    CollectionBanner,
    ProductSlider,
    Banner,
    ProductTab,
    Services,
    Blog,
    Instagram,
    LogoSlider,
    Footer,
    quickviewModel,
    compareModel,
    cartModel,
    newsletterModel,
    CountDown
  },
  data() {
    return {
      products: [],
      category: [],
      showquickviewmodel: false,
      showcomparemodal: false,
      showcartmodal: false,
      quickviewproduct: {},
      comapreproduct: {},
      cartproduct: {}
    }
  },
  computed: {
    ...mapState({
      productslist: state => state.products.productslist
    })
  },
  mounted() {
    this.productsArray()
  
  },
  methods: {
    productsArray: function () {
      this.productslist.map((item) => {
        if (item.type === 'fashion') {
          this.products.push(item)
          item.collection.map((i) => {
            const index = this.category.indexOf(i)
            if (index === -1) this.category.push(i)
          })
        }
      })
    },
    showQuickview(item, productData) {
      this.showquickviewmodel = item
      this.quickviewproduct = productData
    },
    showCoampre(item, productData) {
      this.showcomparemodal = item
      this.comapreproduct = productData
    },
    closeCompareModal(item) {
      this.showcomparemodal = item
    },
    showCart(item, productData) {
      this.showcartmodal = item
      this.cartproduct = productData
    },
    closeCartModal(item) {
      this.showcartmodal = item
    }
  }
}
</script>
