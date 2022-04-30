<template>
  <div class="product">
    <HeaderShop/>
    <!-- karena tidak menggunakan ke halaman yang berbeda -->
        <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section text-left">
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="breadcrumb-text product-more">
                        <router-link to="/">
                            <i class="fa fa-home"></i> 
                            Home
                        </router-link>
                        <span>Detail</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Product Shop Section Begin -->
    <section class="product-shop spad page-details text-left">
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="row">
                        <div class="col-lg-6">
                            <div class="product-pic-zoom">
                                <img class="product-big-img" :src="gambar_default" alt="" />
                            </div>
                            <div class="product-thumbs">
                                <carousel :dots="false" :nav="false" class="product-thumbs-track ps-slider">                                    

                                    <div class="pt active" @click="changeImage(thumbs[0])" >
                                        <img src="img/ck-1.jpg" alt="" />
                                    </div>

                                    <div class="pt" @click="changeImage(thumbs[1])" >
                                        <img src="img/ck-2.jpg" alt="" />
                                    </div>

                                    <div class="pt" @click="changeImage(thumbs[2])">
                                        <img src="img/ck-3.jpg" alt="" />
                                    </div>

                                    <div class="pt" @click="changeImage(thumbs[3])">
                                        <img src="img/ck-4.jpg" alt="" />
                                    </div>
                                </carousel>
                            </div>
                        </div>
                        <div class="col-lg-6">
                            <div class="product-details">
                                <div class="pd-title">
                                    <span>{{ productDetails.type }}</span>
                                    <h3>{{ productDetails.name }}</h3>
                                </div>
                                <div class="pd-desc">
                                    <p>
                                        {{ productDetails.description }}
                                    </p>
                                    <h4>${{ productDetails.price }}</h4>
                                </div>
                                <div class="quantity">
                                    <router-link to="/cart">
                                        <a href="shopping-cart.html" class="primary-btn pd-cart">Add To Cart</a>
                                    </router-link>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
    <!-- Product Shop Section End -->
    <RelatedShop/>


    <FooterShop/>

  </div>
</template>

<script>
// @ is an alias to /src
import HeaderShop from '@/components/HeaderShop.vue'
import RelatedShop from '@/components/RelatedShop.vue'
import FooterShop from '@/components/FooterShop.vue'
import carousel from "vue-owl-carousel"
import axios from 'axios'

export default {
    name: 'ProductView',
    components: {
        HeaderShop,
        RelatedShop,
        FooterShop,
        carousel
    },
    data(){
        return{
            gambar_default: "",
            thumbs : [
                    "img/ck-1.jpg",
                    "img/ck-2.jpg",
                    "img/ck-3.jpg",
                    "img/ck-4.jpg"
            ],
            productDetails: []
        };
    },
    methods : {
        changeImage(img){
            this.gambar_default = img;
            // eslint-disable-next-line no-console
            console.log(this.id);

        },
        setDataPictures(data){
            // replace object productDetails with data dari API
            this.productDetails = data;
            // replace value gambar_default dengan data dari API {galleris}
            this.gambar_default = data.galleries[0].photo;

        }
    },
    mounted() {
        axios
        .get("http://shayna-backend.belajarkoding.com/api/products",{
            params: {
                id: this.$route.params.id
            }
        })
        .then(res => this.setDataPictures(res.data.data))
        // eslint-disable-next-line no-console
        .catch(err => console.log(err));
  },
};
</script>

<style scoped>
.product-thumbs .pt {
    margin-right: 10px;
}
</style>