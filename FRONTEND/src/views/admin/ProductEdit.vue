<template>
    <div v-if="product" class="page">
        <h4>Hiệu Chỉnh Món Ăn</h4>
        <ProductForm :product="product" :categories="categories" @submit:product="updateProduct" />
    </div>
</template>

<script>
import { defineComponent, reactive, toRefs, onMounted } from "vue";
import ProductForm from "@/components/admin/ProductForm.vue";
import ProductService from "@/services/product.service";
import CategoryService from "@/services/category.service";
import { useRouter } from "vue-router"

export default defineComponent({
    components: {
        ProductForm,
    },
    props: {
        id: { type: String, required: true },
    },
    setup(props, context) {

        const state = reactive({
            product: null,
            categories: [],
        });
        const router = useRouter();

        const onFileChange = (event) => {
            const formData = new FormData();
            formData.append("image", event.target.files[0]);
            state.product.image = formData;
        };

        const getProduct = async () => {
            try {
                state.product = await ProductService.get(props.id);
            } catch (error) {
                console.log(error);
            }
        };
        const getCategories = async () => {
            try {
                state.categories = await CategoryService.all();
            } catch (error) {
                console.log(error);
            }
        };
        const updateProduct = async (data) => {
            const formData = new FormData();
            formData.append("name", data.name);
            formData.append("description", data.description);
            formData.append("price", data.price);
            formData.append("quantity", data.quantity);
            formData.append("category_id", data.category_id);
            if (data.image instanceof File) {
                formData.append("image", data.image);
            }
            try {
                await ProductService.update(props.id, formData);
                router.push({ name: "admin.product.all" });
            } catch (error) {
                console.log(error);
            }
        };
        onMounted(async () => {
            await getProduct();
            await getCategories();
        });

        return {
            ...toRefs(state),
            onFileChange,
            updateProduct,
        };
    },
});
</script>
