<script>
  import * as yup from "yup";
  import { Form, Field, ErrorMessage } from "vee-validate";
  export default{
      props:{
          product: { type: Object, required: true },
          resetAfterSubmit: { type: Boolean, default: false },
      }
      ,
     data() {
        const productform = yup.object().shape({
            name: yup
            .string()
            .required("Tên phải có giá trị.")
            .min(5, "Tên phải ít nhất 5 ký tự."),
             img: yup
            .string()
            .required("Hình ảnh phải có giá trị."),
            price: yup
            .string()
            .required("Lượt xem phải có giá trị."),
            description: yup
            .string()
            .required("Mô tả truyện không được để trống.")
            .min(5, "Tên phải ít nhất 5 ký tự."),
            category: yup
            .string()
            .required("Thể loại không được để trống."),
            size: yup
            .string()
            .required("Tình trạng truyện không được để trống."),
            color: yup
            .string()
            .required("Tên tác giả không được để trống."),
            });
            return {
            productLocal:this.product,
            productform,
            }
        },
    components:{
      Form,
      Field,
      ErrorMessage
    },
    emits:['submit:product'],
    methods:{
      addImge(){
        document.querySelector("#imgproduct2").style.display = "block";
      },
      submitproduct(){
          this.$emit('submit:product',this.productLocal);
          	if (this.resetAfterSubmit) {
				    this.$refs.contactForm.resetForm();
			  }
      },
    }
  }
</script>
<template>
<div class="wrapper">
    <Form :validation-schema="productform"  @submit="submitproduct" >
      <div class="form-group">
        <label for="nameproduct">Tên truyện</label>
        <Field type="text" class="form-control" id="nameproduct" name="name" placeholder="Nhập tên truyện" v-model="productLocal.title" />
        <ErrorMessage name="name" class="text-danger" />
      </div>
    <div class="form-group">
        <label for="imgproduct">Image</label>
        <div style="display: flex; flex-direction: row;">
        <Field type="text" class="form-control" id="imgproduct" name="img" placeholder="Nhập link ảnh truyện" v-model="productLocal.img[0]"/>
        </div>

      </div>
      <div class="form-group">
        <label for="priceproduct">Lượt xem</label>
        <Field type="number" class="form-control" id="priceproduct" name="price" placeholder="Nhập số lượt xem" v-model="productLocal.price" />
        <ErrorMessage name="price" class="text-danger"  />
      </div>
      <div class="form-group">
        <label for="nameproduct">Tóm tắt truyện</label>
        <Field type="text" class="form-control" id="nameproduct" name="description"  placeholder="Nhập mô tả truyện" v-model="productLocal.desc"/>
          <ErrorMessage name="description" class="text-danger" />
      </div>
      <div class="form-group">
        <label for="categoryproduct">Thể loại</label>
        <Field type="text" class="form-control" id="categoryproduct" name="category" placeholder="Nhập thể loại" v-model="productLocal.categories"/>
          <ErrorMessage name="category" class="text-danger" />
      </div>
      <div class="form-group">
        <label for="sizeproduct">Tình trạng truyện</label>
        <Field type="text" class="form-control" id="sizeproduct" name="size" placeholder="Nhập trình trạng truyện" v-model="productLocal.size"/>
          <ErrorMessage name="size" class="text-danger" />
      </div>
       <div class="form-group">
        <label for="colorproduct">Tên tác giả</label>
        <Field type="text" class="form-control" id="colorproduct" name="color"  placeholder="Nhập tên tác giả" v-model="productLocal.color"/>
          <ErrorMessage name="color" class="text-danger" />
      </div>
      <button type="submit" class="btn btn-primary">Lưu</button>
       <router-link to="/admin" style="margin: 10px;">
            <button class="btn btn-danger">Trở về</button>
        </router-link>
      <br>
    </Form>
</div>
</template>
<style scoped>
.wrapper{
    margin: 50px 200px;
}
.btn_img-add{
 font-size: 30px; 
 color: dodgerblue;
}
</style>