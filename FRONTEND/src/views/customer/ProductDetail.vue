<template>
    <div v-if="product" class="page">
        <div class="container mb-1">
            <div class="row pt-5 ">
                <div class="col-sm-12 col-md-12 col-lg-5 text-center">
                    <img style="height:400px" :src="'http://localhost:3000/' + product.image" />
                </div>
                <div class="col-sm-10 col-md-12 col-lg-7 pb-2">
                    <header>
                        <div class="flex justify-center absolute items-center w-full flex-col">
                            <span class="text-secondary text-lg">
                                <router-link tag="span" class="text-lg cursor-pointer" to="/">
                                    Trang chủ
                                </router-link>
                                <router-link tag="span" class="text-lg cursor-pointer" to="/">
                                    / Sản phẩm/
                                </router-link>
                                {{ product.name }}
                            </span>
                        </div>
                    </header>
                    <div class="row">
                        <h3 class="pb-0 mb-3 col-12">
                            {{ product.name }}
                            <button class="btn btn-primary btn-sm text-white ms-4">{{ category.name }}</button>
                        </h3>
                    </div>

                    <div class="row">
                        <h2 class="col-3 text-danger">
                            {{ formatPrice(product.price) }}
                        </h2>
                        <p class="col-3 mb-0 pb-0"><i class="fa-solid fa-star"></i>
                            <i class="fa-solid fa-star"></i>
                            <i class="fa-solid fa-star"></i>
                            <i class="fa-solid fa-star"></i>
                            <i class="fa-solid fa-star"></i>
                        </p>
                    </div>
                    <p>
                    </p>
                    <div class="row">
                        <p class="col-6"><b>Đã bán: </b>
                            {{ product.quantity_sale }}</p>
                    </div>
                    <p>
                        {{ product.description }}
                    </p>
                    <hr>

                    <p class="fw-bold col-3">SỐ LƯỢNG</p>
                    <div class="row ps-3"><input type="number" class="col-1 text-center" v-model="quantity_sale" min="1"
                            :max="product.quantity_remain" />
                        <p class="col-3 mb-0 text-muted">Còn Lại / Phần :
                            {{ product.quantity_remain }}
                        </p>
                    </div>
                    <button class="btn-danger btn mt-3" @click="addToCart(
                        {
                            _id: product._id,
                            name: product.name,
                            description: product.description,
                            price: product.price,
                            image: product.image,
                            quantity_sale: quantity_sale,
                            category_id: product.category_id,
                        }
                    )" :disabled="product.quantity_remain === 0 || quantity_sale > product.quantity">

                        <i class="fas fa-cart-plus"> </i> Thêm vào giỏ
                    </button>
                </div>
            </div>
        </div>
        <h4 class="container mt-5 mb-2">Các món ăn liên quan</h4>
        <div class="container col-12 ms-5 ps-4">
            <ProductCard v-if="state.products.length > 0" :products="state.products" />
            <div v-else class="text-center">Loading...</div>
        </div>

        
        <section class="container py-4" v-if="selectedProduct">
        <div class="row">
            <div class="col-md-12">
            <h4>{{ selectedProduct.name }}</h4>
            <ul id="tabs" class="nav nav-tabs">
                <li class="nav-item">
                <a href="#" data-target="#home1" data-toggle="tab" class="nav-link small text-uppercase active">Công Thức</a>
                </li>
            </ul>
            <br>
            <div id="tabsContent" class="tab-content pb-5">
                <div id="home1" class="tab-pane fade active show">
                <div class="row pb-2">
                    <div class="col-md-7">
                   

                

                        <p><strong>Nguyên Liệu:</strong> {{ selectedProduct.ingredients }}</p>
                        
                        <p v-if="selectedProduct.name === 'Lẩu gà ớt hiểm' || 
                            selectedProduct.name === 'Lẩu cá thác lác' || 
                            selectedProduct.name === 'Lẩu bần' ||
                            selectedProduct.name === 'Lẩu cá kèo' ||  
                            selectedProduct.name === 'Lẩu cá linh theo mùa' || 
                            selectedProduct.name === 'Lẩu vịt nấu chao' || 
                            selectedProduct.name === 'Lẩu mắm' ||
                            selectedProduct.name === 'Lẩu riêu cua'">
                            <strong>+</strong> {{ selectedProduct.ingredients1 }}
                        </p>

                        <p v-if="selectedProduct.name === 'Lẩu gà ớt hiểm' || 
                            selectedProduct.name === 'Lẩu cá thác lác' || 
                            selectedProduct.name === 'Lẩu bần' ||
                            selectedProduct.name === 'Lẩu cá kèo' ||  
                            selectedProduct.name === 'Lẩu cá linh theo mùa' || 
                            selectedProduct.name === 'Lẩu vịt nấu chao' || 
                            selectedProduct.name === 'Lẩu mắm' ||
                            selectedProduct.name === 'Lẩu riêu cua'">
                            <strong>+</strong> {{ selectedProduct.ingredients2 }}
                        </p>

                        <p v-if="selectedProduct.name === 'Lẩu gà ớt hiểm' || 
                            selectedProduct.name === 'Lẩu cá thác lác' || 
                            selectedProduct.name === 'Lẩu bần' ||
                            selectedProduct.name === 'Lẩu cá kèo' ||  
                            selectedProduct.name === 'Lẩu cá linh theo mùa' || 
                            selectedProduct.name === 'Lẩu vịt nấu chao' || 
                            selectedProduct.name === 'Lẩu mắm' ||
                            selectedProduct.name === 'Lẩu riêu cua'">
                            <strong>+</strong> {{ selectedProduct.ingredients3 }}
                        </p>

                        <p v-if="selectedProduct.name === 'Lẩu gà ớt hiểm' || 
                            selectedProduct.name === 'Lẩu cá thác lác' || 
                            selectedProduct.name === 'Lẩu bần' ||
                            selectedProduct.name === 'Lẩu cá kèo' ||  
                            selectedProduct.name === 'Lẩu cá linh theo mùa' || 
                            selectedProduct.name === 'Lẩu vịt nấu chao' || 
                            selectedProduct.name === 'Lẩu mắm' ||
                            selectedProduct.name === 'Lẩu riêu cua'">
                            <strong>+</strong> {{ selectedProduct.ingredients4 }}
                        </p>

                        <p v-if="selectedProduct.name === 'Lẩu gà ớt hiểm' || 
                            selectedProduct.name === 'Lẩu cá thác lác' || 
                            selectedProduct.name === 'Lẩu bần' ||
                            selectedProduct.name === 'Lẩu cá kèo' ||  
                            selectedProduct.name === 'Lẩu cá linh theo mùa' || 
                            selectedProduct.name === 'Lẩu vịt nấu chao' || 
                            selectedProduct.name === 'Lẩu mắm' ||
                            selectedProduct.name === 'Lẩu riêu cua'">
                            <strong>+</strong> {{ selectedProduct.ingredients5 }}
                        </p>

                        <p v-if="selectedProduct.name === 'Lẩu gà ớt hiểm' || 
                            selectedProduct.name === 'Lẩu cá thác lác' || 
                            selectedProduct.name === 'Lẩu bần' ||
                            selectedProduct.name === 'Lẩu cá kèo' ||  
                            selectedProduct.name === 'Lẩu cá linh theo mùa' || 
                            selectedProduct.name === 'Lẩu vịt nấu chao' || 
                            selectedProduct.name === 'Lẩu mắm' ||
                            selectedProduct.name === 'Lẩu riêu cua'">
                            <strong>+</strong> {{ selectedProduct.ingredients6 }}
                        </p>

                        <p v-if="selectedProduct.name === 'Lẩu gà ớt hiểm' || 
                            selectedProduct.name === 'Lẩu cá thác lác' || 
                            selectedProduct.name === 'Lẩu bần' ||
                            selectedProduct.name === 'Lẩu cá kèo' ||  
                            selectedProduct.name === 'Lẩu cá linh theo mùa' || 
                            selectedProduct.name === 'Lẩu vịt nấu chao' || 
                            selectedProduct.name === 'Lẩu mắm' ||
                            selectedProduct.name === 'Lẩu riêu cua'">
                            <strong>+</strong> {{ selectedProduct.ingredients7 }}
                        </p>

                        <p v-if="selectedProduct.name === 'Lẩu gà ớt hiểm' || 
                            selectedProduct.name === 'Lẩu cá thác lác' || 
                            selectedProduct.name === 'Lẩu bần' ||
                            selectedProduct.name === 'Lẩu cá kèo' ||  
                            selectedProduct.name === 'Lẩu cá linh theo mùa' || 
                            selectedProduct.name === 'Lẩu vịt nấu chao' || 
                            selectedProduct.name === 'Lẩu mắm' ||
                            selectedProduct.name === 'Lẩu riêu cua'">
                            <strong>+</strong> {{ selectedProduct.ingredients8 }}
                        </p>

                        <p v-if="selectedProduct.name === 'Lẩu gà ớt hiểm' || 
                            selectedProduct.name === 'Lẩu cá thác lác' || 
                            selectedProduct.name === 'Lẩu bần' ||
                            selectedProduct.name === 'Lẩu cá kèo' ||  
                            selectedProduct.name === 'Lẩu cá linh theo mùa' || 
                            selectedProduct.name === 'Lẩu vịt nấu chao' || 
                            selectedProduct.name === 'Lẩu mắm' ||
                            selectedProduct.name === 'Lẩu riêu cua'">
                            <strong>+</strong> {{ selectedProduct.ingredients9 }}
                        </p>

                        <p v-if="selectedProduct.name === 'Lẩu gà ớt hiểm' || 
                            selectedProduct.name === 'Lẩu cá thác lác' || 
                            selectedProduct.name === 'Lẩu bần' ||
                            selectedProduct.name === 'Lẩu cá kèo' ||  
                            selectedProduct.name === 'Lẩu cá linh theo mùa' || 
                            selectedProduct.name === 'Lẩu vịt nấu chao' || 
                            selectedProduct.name === 'Lẩu mắm' ||
                            selectedProduct.name === 'Lẩu riêu cua'">
                            <strong>+</strong> {{ selectedProduct.ingredients10 }}
                        </p>

                        <p v-if="selectedProduct.name === 'Lẩu gà ớt hiểm' || 
                            selectedProduct.name === 'Lẩu cá thác lác' || 
                            selectedProduct.name === 'Lẩu bần' ||
                            selectedProduct.name === 'Lẩu cá kèo' ||  
                            selectedProduct.name === 'Lẩu cá linh theo mùa' || 
                            selectedProduct.name === 'Lẩu vịt nấu chao' || 
                            selectedProduct.name === 'Lẩu mắm' ||
                            selectedProduct.name === 'Lẩu riêu cua'">
                            <strong>+</strong> {{ selectedProduct.ingredients11 }}
                        </p>

                        <p v-if="selectedProduct.name === 'Lẩu gà ớt hiểm' || 
                            selectedProduct.name === 'Lẩu cá thác lác' || 
                            selectedProduct.name === 'Lẩu bần' ||
                            selectedProduct.name === 'Lẩu cá kèo' ||  
                            selectedProduct.name === 'Lẩu cá linh theo mùa' || 
                            selectedProduct.name === 'Lẩu vịt nấu chao' || 
                            selectedProduct.name === 'Lẩu mắm' ||
                            selectedProduct.name === 'Lẩu riêu cua'">
                            <strong>+</strong> {{ selectedProduct.ingredients12 }}
                        </p>

                        <p v-if="selectedProduct.name === 'Lẩu gà ớt hiểm' || 
                            selectedProduct.name === 'Lẩu cá thác lác' || 
                            selectedProduct.name === 'Lẩu cá kèo' ||  
                            selectedProduct.name === 'Lẩu cá linh theo mùa' || 
                            selectedProduct.name === 'Lẩu vịt nấu chao' || 
                            selectedProduct.name === 'Lẩu mắm' ||
                            selectedProduct.name === 'Lẩu riêu cua'">
                            <strong>+</strong> {{ selectedProduct.ingredients13 }}
                        </p>

                  

                        <p><strong>Cách Làm: </strong><span v-html="selectedProduct.description"></span></p>

                        <p v-if="selectedProduct.name === 'Lẩu gà ớt hiểm' || 
                            selectedProduct.name === 'Lẩu cá thác lác' || 
                            selectedProduct.name === 'Lẩu bần' ||
                            selectedProduct.name === 'Lẩu cá kèo' ||  
                            selectedProduct.name === 'Lẩu cá linh theo mùa' || 
                            selectedProduct.name === 'Lẩu vịt nấu chao' || 
                            selectedProduct.name === 'Lẩu mắm' ||
                            selectedProduct.name === 'Lẩu riêu cua'">
                            <strong>1: </strong><span v-html="selectedProduct.description1"></span>
                        </p>

                        <p v-if="selectedProduct.name === 'Lẩu gà ớt hiểm' || 
                            selectedProduct.name === 'Lẩu cá thác lác' || 
                            selectedProduct.name === 'Lẩu bần' ||
                            selectedProduct.name === 'Lẩu cá kèo' ||  
                            selectedProduct.name === 'Lẩu cá linh theo mùa' || 
                            selectedProduct.name === 'Lẩu vịt nấu chao' || 
                            selectedProduct.name === 'Lẩu mắm' ||
                            selectedProduct.name === 'Lẩu riêu cua'">
                            <strong>2: </strong><span v-html="selectedProduct.description2"></span>
                        </p>

                        <p v-if="selectedProduct.name === 'Lẩu gà ớt hiểm' || 
                            selectedProduct.name === 'Lẩu cá thác lác' || 
                            selectedProduct.name === 'Lẩu bần' ||
                            selectedProduct.name === 'Lẩu cá kèo' ||  
                            selectedProduct.name === 'Lẩu cá linh theo mùa' || 
                            selectedProduct.name === 'Lẩu vịt nấu chao' || 
                            selectedProduct.name === 'Lẩu mắm' ||
                            selectedProduct.name === 'Lẩu riêu cua'">
                            <strong>3: </strong><span v-html="selectedProduct.description3"></span>
                        </p>

                        <p v-if="selectedProduct.name === 'Lẩu gà ớt hiểm' || 
                            selectedProduct.name === 'Lẩu cá thác lác' || 
                            selectedProduct.name === 'Lẩu bần' ||
                            selectedProduct.name === 'Lẩu cá kèo' ||  
                            selectedProduct.name === 'Lẩu cá linh theo mùa' || 
                            selectedProduct.name === 'Lẩu vịt nấu chao' || 
                            selectedProduct.name === 'Lẩu mắm' ||
                            selectedProduct.name === 'Lẩu riêu cua'">
                            <strong>4: </strong><span v-html="selectedProduct.description4"></span>
                        </p>

                        <p v-if="selectedProduct.name === 'Lẩu gà ớt hiểm' || 
                            selectedProduct.name === 'Lẩu cá thác lác' || 
                            selectedProduct.name === 'Lẩu bần' ||
                            selectedProduct.name === 'Lẩu cá kèo' ||  
                            selectedProduct.name === 'Lẩu cá linh theo mùa' || 
                            selectedProduct.name === 'Lẩu vịt nấu chao' || 
                            selectedProduct.name === 'Lẩu mắm' ||
                            selectedProduct.name === 'Lẩu riêu cua'">
                            <strong>5: </strong><span v-html="selectedProduct.description5"></span>
                        </p>

                        <p v-if="selectedProduct.name === 'Lẩu gà ớt hiểm' || 
                            selectedProduct.name === 'Lẩu cá thác lác' || 
                            selectedProduct.name === 'Lẩu bần' ||
                            selectedProduct.name === 'Lẩu cá kèo' ||  
                            selectedProduct.name === 'Lẩu cá linh theo mùa' || 
                            selectedProduct.name === 'Lẩu vịt nấu chao' || 
                            selectedProduct.name === 'Lẩu mắm' ||
                            selectedProduct.name === 'Lẩu riêu cua'">
                            <strong>6: </strong><span v-html="selectedProduct.description6"></span>
                        </p>

                        <p v-if="selectedProduct.name === 'Lẩu gà ớt hiểm' ||  
                            selectedProduct.name === 'Lẩu bần' ||  
                            selectedProduct.name === 'Lẩu cá linh theo mùa' || 
                            selectedProduct.name === 'Lẩu vịt nấu chao' || 
                            selectedProduct.name === 'Lẩu mắm' ||
                            selectedProduct.name === 'Lẩu riêu cua'">
                            <strong>7: </strong><span v-html="selectedProduct.description7"></span>
                        </p>

                  

                    </div>
                </div>
                </div>
            </div>
            </div>
        </div>
        </section>

        <section class="container py-4" v-if="!selectedProduct">
        <div class="row">
            <div class="col-md-12">
            <h4>Chọn món ăn để xem công thức</h4>
            <div class="row">
                <div class="col-md-4" v-for="product in products" :key="product.name" @click="showProductDetails(product)">
                <div class="card mb-4 shadow-sm" :class="{ 'active': selectedIndex === index }">
                    <div class="card-body">
                    <h5 class="card-title">{{ product.name }}</h5>
                    <p class="card-text" v-html="description"></p>
                    </div>
                </div>
                </div>
            </div>
            </div>
        </div>
        </section>

        <!-- <div class="product-details">
            <img :src="'http://localhost:3000/' + product.image" alt="" />

            <div class="product-info">
                <h5>{{ product.name }}</h5>
                <p>{{ product.description }}</p>
                <p>Giá: {{ product.price }}</p>
                <p>Số lượng còn lại: {{ product.quantity_remain }}</p>
                <input type="number" class="form-control" v-model="quantity_sale" min="1" :max="product.quantity_remain" />
                <button class="btn-cart btn " @click="addToCart(
                    {
                        _id: product._id,
                        name: product.name,
                        description: product.description,
                        price: product.price,
                        image: product.image,
                        quantity_sale: quantity_sale,
                        category_id: product.category_id,
                    }
                )" :disabled="product.quantity_remain === 0 || quantity_sale > product.quantity">

                    <i class="fas fa-cart-plus"></i> Thêm vào giỏ
                </button>
            </div>
        </div> -->

        
    </div>
</template>
  
<script>
import { defineComponent, onMounted, ref, reactive, computed } from 'vue';
import ProductService from '@/services/product.service';
import CategoryService from '@/services/category.service';
import { useRouter } from "vue-router";
import CustomerService from "@/services/customer.service";
import ProductCard from '@/components/customer/ProductCard.vue';
import { useCustomerStore } from '@/stores/store';
import { useToast } from 'vue-toast-notification';

export default defineComponent({
    data() {
    return {
      products: [
        {
            name: 'Lẩu gà ớt hiểm',
            img: '/src/assets/img/about3.png',
            description: '',
            description1: 'Phi thơm tỏi, gừng, sả trong chút dầu ăn.',
            description2: 'Cho thịt gà vào, xào cho săn lại.',
            description3: 'Thêm ớt sừng bò, cà chua, nước dùng và một ít nước cốt chanh.',
            description4: 'Nêm nếm gia vị (muối, đường, bột ngọt) cho vừa ăn.',
            description5: 'Khi sôi, cho rau ngổ, rau răm vào và đun sôi trong 5-7 phút.',
            description6: 'Cuối cùng, cho hẹ vào, nêm nếm lại cho vừa ăn.',
            description7: 'Múc lẩu ra tô, ăn nóng cùng rau muống, rau cần, rau thơm.',
            ingredients: '',
            ingredients1: '1 con gà, thái miếng vừa ăn',
            ingredients2: '200g ớt sừng bò, băm nhỏ',
            ingredients3: '4 tép tỏi, băm nhỏ',
            ingredients4: '2 thìa gừng, băm nhỏ',
            ingredients5: '2 quả chanh, vắt lấy nước',
            ingredients6: '2 cọng sả, băm nhỏ',
            ingredients7: '2 quả cà chua, thái múng',
            ingredients8: '2 củ hẹ, thái khúc',
            ingredients9: '1 nắm rau răm, rửa sạch, xé nhỏ',
            ingredients10: '1 nắm rau ngổ, rửa sạch, xé nhỏ',
            ingredients11: 'Nước dùng (khoảng 2 lít)',
            ingredients12: 'Muối, đường, bột ngọt, dầu ăn',
            ingredients13: 'Rau muống, rau cần, rau thơm để ăn kèm'
        },
        {
            name: 'Lẩu cá thác lác',
            img: '/src/assets/img/about3.png',
            description: '',
            description1: 'Cho các thác lác vào nồi, đổ nước dùng vừa đủ để ngập các thác lác.',
            description2: 'Đun sôi, sau đó hạ lửa nhỏ và nấu trong khoảng 15-20 phút cho đến khi các thác lác chín mềm.',
            description3: 'Thêm hành tím, tỏi, sả, gừng và ớt vào nồi, tiếp tục nấu khoảng 5 phút.',
            description4: 'Nêm nếm với nước mắm, đường, bột ngọt và muối cho vừa ăn.',
            description5: 'Cuối cùng, cho lá lốt, rau ngổ và rau muống vào nồi, nấu thêm 2-3 phút cho rau chín.',
            description6: 'Múc lẩu ra bát, thưởng thức nóng hổi cùng cơm trắng.',
            ingredients: '',
            ingredients1: '500g các thác lác tươi, rửa sạch, để ráo',
            ingredients2: '1 củ hành tím, lạng lớp vỏ ngoài, cắt lát',
            ingredients3: '3-4 tép tỏi, bóc vỏ, băm nhỏ',
            ingredients4: '1 nhánh sả, bóc vỏ, băm nhỏ',
            ingredients5: '1 lát gừng tươi, băm nhỏ',
            ingredients6: '2 quả ớt chỉ thiên, băm nhỏ',
            ingredients7: '2 lá lốt, rửa sạch, xé nhỏ',
            ingredients8: '1 bó rau ngổ, rửa sạch, thái nhỏ',
            ingredients9: '1 bó rau muống, rửa sạch, thái đoạn khoảng 5cm',
            ingredients10: '1 thìa canh đường',
            ingredients11: '1 thìa cà phê bột ngọt',
            ingredients12: '1 thìa cà phê muối',
            ingredients13: '1 lít nước dùng (có thể dùng nước lèo hoặc nước xương)'
        },
        {
            name: 'Lẩu bần',
            img: '/src/assets/img/about3.png',
            description: '',
            description1: 'Phi thơm tỏi, gừng, sả trong chút dầu ăn.',
            description2: 'Cho thịt gà vào, xào cho săn lại.',
            description3: 'Thêm ớt sừng bò, cà chua, nước dùng và một ít nước cốt chanh.',
            description4: 'Nêm nếm gia vị (muối, đường, bột ngọt) cho vừa ăn.',
            description5: 'Khi sôi, cho rau ngổ, rau răm vào và đun sôi trong 5-7 phút.',
            description6: 'Cuối cùng, cho hẹ vào, nêm nếm lại cho vừa ăn.',
            description7: 'Múc lẩu ra tô, ăn nóng cùng rau muống, rau cần, rau thơm.',
            ingredients: '',
            ingredients1: '500g bần tươi, rửa sạch, cắt khúc khoảng 5cm',
            ingredients2: '1 củ hành tím, lạng lớp vỏ ngoài, cắt lát',
            ingredients3: '3-4 tép tỏi, bóc vỏ, băm nhỏ',
            ingredients4: '2 quả ớt chỉ thiên, băm nhỏ',
            ingredients5: '1 lá chanh, băm nhỏ',
            ingredients6: '1 bó rau đắng, rửa sạch, thái nhỏ',
            ingredients7: '1 bó rau ngót, rửa sạch, thái nhỏ',
            ingredients8: '1 thìa canh nước mắm',
            ingredients9: '1 thìa canh đường',
            ingredients10: '1 thìa cà phê bột ngọt',
            ingredients11: '1 thìa cà phê muối',
            ingredients12: '1 lít nước dùng (có thể dùng nước lèo hoặc nước xương)'
        },
        {
            name: 'Lẩu cá kèo',
            img: '/src/assets/img/about3.png',
            description: '',
            description1: 'Cho cá kèo vào nồi, đổ nước dùng vừa đủ để ngập cá.',
            description2: 'Đun sôi, sau đó hạ lửa nhỏ và nấu trong khoảng 10-15 phút cho đến khi cá chín.',
            description3: 'Thêm hành tím, tỏi, gừng và ớt chỉ thiên vào nồi, tiếp tục nấu khoảng 5 phút.',
            description4: 'Nêm nếm với nước mắm, đường, bột ngọt và muối cho vừa ăn.',
            description5: 'Cuối cùng, cho rau muống, rau đắng và rau ngổ vào nồi, nấu thêm 2-3 phút cho rau chín.',
            description6: 'Múc lẩu ra bát, thưởng thức nóng hổi cùng cơm trắng.',
            ingredients: '',
            ingredients1: '500g cá kèo tươi, rửa sạch, cắt khoanh 5cm',
            ingredients2: '1 củ hành tím, lạng lớp vỏ ngoài, cắt lát',
            ingredients3: '3-4 tép tỏi, bóc vỏ, băm nhỏ',
            ingredients4: '1 lát gừng tươi, băm nhỏ',
            ingredients5: '2 quả ớt chỉ thiên, cắt lát',
            ingredients6: '1 bó rau muống, rửa sạch, thái đoạn khoảng 5cm',
            ingredients7: '1 bó rau đắng, rửa sạch, thái nhỏ',
            ingredients8: '1 bó rau ngổ, rửa sạch, thái nhỏ',
            ingredients9: '1 thìa canh nước mắm',
            ingredients10: '1 thìa canh đường',
            ingredients11: '1 thìa cà phê bột ngọt',
            ingredients12: '1 thìa cà phê muối',
            ingredients13: '1 lít nước dùng (có thể dùng nước lèo hoặc nước xương)'
        },
        {
            name: 'Lẩu cá linh theo mùa',
            img: '/src/assets/img/about3.png',
            description: '',
            description1: 'Phi thơm tỏi, gừng, sả trong chút dầu ăn.',
            description2: 'Cho thịt gà vào, xào cho săn lại.',
            description3: 'Thêm ớt sừng bò, cà chua, nước dùng và một ít nước cốt chanh.',
            description4: 'Nêm nếm gia vị (muối, đường, bột ngọt) cho vừa ăn.',
            description5: 'Khi sôi, cho rau ngổ, rau răm vào và đun sôi trong 5-7 phút.',
            description6: 'Cuối cùng, cho hẹ vào, nêm nếm lại cho vừa ăn.',
            description7: 'Múc lẩu ra tô, ăn nóng cùng rau muống, rau cần, rau thơm.',
            ingredients: '',
            ingredients1: '1 con gà, thái miếng vừa ăn',
            ingredients2: '200g ớt sừng bò, băm nhỏ',
            ingredients3: '4 tép tỏi, băm nhỏ',
            ingredients4: '2 thìa gừng, băm nhỏ',
            ingredients5: '2 quả chanh, vắt lấy nước',
            ingredients6: '2 cọng sả, băm nhỏ',
            ingredients7: '2 quả cà chua, thái múng',
            ingredients8: '2 củ hẹ, thái khúc',
            ingredients9: '1 nắm rau răm, rửa sạch, xé nhỏ',
            ingredients10: '1 nắm rau ngổ, rửa sạch, xé nhỏ',
            ingredients11: 'Nước dùng (khoảng 2 lít)',
            ingredients12: 'Muối, đường, bột ngọt, dầu ăn',
            ingredients13: 'Rau muống, rau cần, rau thơm để ăn kèm'
        },
        {
            name: 'Lẩu vịt nấu chao',
            img: '/src/assets/img/about3.png',
            description: '',
            description1: 'Phi thơm tỏi, gừng, sả trong chút dầu ăn.',
            description2: 'Cho thịt gà vào, xào cho săn lại.',
            description3: 'Thêm ớt sừng bò, cà chua, nước dùng và một ít nước cốt chanh.',
            description4: 'Nêm nếm gia vị (muối, đường, bột ngọt) cho vừa ăn.',
            description5: 'Khi sôi, cho rau ngổ, rau răm vào và đun sôi trong 5-7 phút.',
            description6: 'Cuối cùng, cho hẹ vào, nêm nếm lại cho vừa ăn.',
            description7: 'Múc lẩu ra tô, ăn nóng cùng rau muống, rau cần, rau thơm.',
            ingredients: '',
            ingredients1: '1 con gà, thái miếng vừa ăn',
            ingredients2: '200g ớt sừng bò, băm nhỏ',
            ingredients3: '4 tép tỏi, băm nhỏ',
            ingredients4: '2 thìa gừng, băm nhỏ',
            ingredients5: '2 quả chanh, vắt lấy nước',
            ingredients6: '2 cọng sả, băm nhỏ',
            ingredients7: '2 quả cà chua, thái múng',
            ingredients8: '2 củ hẹ, thái khúc',
            ingredients9: '1 nắm rau răm, rửa sạch, xé nhỏ',
            ingredients10: '1 nắm rau ngổ, rửa sạch, xé nhỏ',
            ingredients11: 'Nước dùng (khoảng 2 lít)',
            ingredients12: 'Muối, đường, bột ngọt, dầu ăn',
            ingredients13: 'Rau muống, rau cần, rau thơm để ăn kèm'
        },
        {
            name: 'Lẩu mắm',
            img: '/src/assets/img/about3.png',
            description: '',
            description1: 'Phi thơm tỏi, gừng, sả trong chút dầu ăn.',
            description2: 'Cho thịt gà vào, xào cho săn lại.',
            description3: 'Thêm ớt sừng bò, cà chua, nước dùng và một ít nước cốt chanh.',
            description4: 'Nêm nếm gia vị (muối, đường, bột ngọt) cho vừa ăn.',
            description5: 'Khi sôi, cho rau ngổ, rau răm vào và đun sôi trong 5-7 phút.',
            description6: 'Cuối cùng, cho hẹ vào, nêm nếm lại cho vừa ăn.',
            description7: 'Múc lẩu ra tô, ăn nóng cùng rau muống, rau cần, rau thơm.',
            ingredients: '',
            ingredients1: '1 con gà, thái miếng vừa ăn',
            ingredients2: '200g ớt sừng bò, băm nhỏ',
            ingredients3: '4 tép tỏi, băm nhỏ',
            ingredients4: '2 thìa gừng, băm nhỏ',
            ingredients5: '2 quả chanh, vắt lấy nước',
            ingredients6: '2 cọng sả, băm nhỏ',
            ingredients7: '2 quả cà chua, thái múng',
            ingredients8: '2 củ hẹ, thái khúc',
            ingredients9: '1 nắm rau răm, rửa sạch, xé nhỏ',
            ingredients10: '1 nắm rau ngổ, rửa sạch, xé nhỏ',
            ingredients11: 'Nước dùng (khoảng 2 lít)',
            ingredients12: 'Muối, đường, bột ngọt, dầu ăn',
            ingredients13: 'Rau muống, rau cần, rau thơm để ăn kèm'
        },
        {
            name: 'Lẩu riêu cua',
            img: '/src/assets/img/about3.png',
            description: '',
            description1: 'Phi thơm tỏi, gừng, sả trong chút dầu ăn.',
            description2: 'Cho thịt gà vào, xào cho săn lại.',
            description3: 'Thêm ớt sừng bò, cà chua, nước dùng và một ít nước cốt chanh.',
            description4: 'Nêm nếm gia vị (muối, đường, bột ngọt) cho vừa ăn.',
            description5: 'Khi sôi, cho rau ngổ, rau răm vào và đun sôi trong 5-7 phút.',
            description6: 'Cuối cùng, cho hẹ vào, nêm nếm lại cho vừa ăn.',
            description7: 'Múc lẩu ra tô, ăn nóng cùng rau muống, rau cần, rau thơm.',
            ingredients: '',
            ingredients1: '1 con gà, thái miếng vừa ăn',
            ingredients2: '200g ớt sừng bò, băm nhỏ',
            ingredients3: '4 tép tỏi, băm nhỏ',
            ingredients4: '2 thìa gừng, băm nhỏ',
            ingredients5: '2 quả chanh, vắt lấy nước',
            ingredients6: '2 cọng sả, băm nhỏ',
            ingredients7: '2 quả cà chua, thái múng',
            ingredients8: '2 củ hẹ, thái khúc',
            ingredients9: '1 nắm rau răm, rửa sạch, xé nhỏ',
            ingredients10: '1 nắm rau ngổ, rửa sạch, xé nhỏ',
            ingredients11: 'Nước dùng (khoảng 2 lít)',
            ingredients12: 'Muối, đường, bột ngọt, dầu ăn',
            ingredients13: 'Rau muống, rau cần, rau thơm để ăn kèm'
        }
      ],
      selectedProduct: null
    }
  },
  mounted() {
    this.showProductDetails(this.products[0]);
  },
  methods: {
    showProductDetails(product) {
      this.selectedProduct = product;
    }
  },


    components: {
        ProductCard,
    },
    props: {
        id: { type: String, required: true },
    },
    mounted() {
        document.title = 'Chi tiết sản phẩm - TuyenFood';
    },
    setup(props) {
        const state = reactive({
            products: [],
        });

        const product = ref(null);
        const category = ref(null);
        const toast = useToast();
        const quantity_sale = ref(1);
        const store = useCustomerStore();
        const router = useRouter();
        const addToCart = async (data) => {
            console.log(data);
            if (store.isAuthenticatedCustomer) {
                try {
                    const response = await CustomerService.addToCart(data);
                    localStorage.setItem("user", JSON.stringify(response.user));
                    toast.success('Thêm vào giỏ hàng thành công!', { timeout: 1500 });
                    //router.push({ name: "cart" });
                }
                catch (error) {
                    console.log(error);
                }
            } else {
                router.push({
                    name: "signin",
                });
            }
        };

        const formatPrice = (price) => {
            return new Intl.NumberFormat('vi-VN', { style: 'currency', currency: 'VND' }).format(price);
        };

        onMounted(async () => {
            product.value = await ProductService.get(props.id);
            category.value = await CategoryService.get(product.value.category_id);
        });
        const retrieveProducts = async () => {
            try {
                product.value = await ProductService.get(props.id);
                console.log("product: " + product);
                console.log("product cate: " + product.value.category_id);
                const products = await ProductService.findByCategory(product.value.category_id);
                state.products = products;
            } catch (error) {
                console.log(error);
            }
        };
        retrieveProducts();
        return {
            state,
            category,
            product,
            formatPrice,
            retrieveProducts,
            addToCart,
            quantity_sale,
        };
    },
});
</script>
<style scoped>
.fa-star {
    color: orange;
    font-size: 16px;
}
.card.active {
  background-color: #f8d7da; /* Màu nền đỏ */
  border-color: #f5c6cb; /* Màu viền đỏ */
}










</style>

  