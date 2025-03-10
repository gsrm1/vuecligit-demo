<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <VForm @submit="onSubmit" v-slot="{ errors, values }">
      {{ errors }} {{ values }}
      <div class="mb-3">
        <VField
          id="email"
          name="email"
          type="email"
          class="form-control"
          rules="email|required"
          v-model="user.email"
          placeholder="請輸入 Email"
          :class="{
            'is-invalid': errors['email'],
            'is-valid': !errors['email'] && user.email,
          }"
        ></VField>
        <!--加上驗證正確效果：is-valid後面加上相反驚嘆號，並且加上user.email讓is-valid在空值時不會被加上去-->
        <!-- 注意：上方的rules不要加bind -->
        <error-message name="email" class="invalid-feedback"></error-message>
      </div>

      <div class="mb-3">
        <VField
          id="name"
          name="姓名"
          type="text"
          class="form-control"
          rules="required"
          v-model="user.name"
          placeholder="請輸入姓名"
          :class="{ 'is-invalid': errors['姓名'] }"
        ></VField>
        <error-message name="姓名" class="invalid-feedback"></error-message>
      </div>

      <div class="mb-3">
        <VField
          id="phone"
          name="phone"
          type="tel"
          class="form-control"
          :rules="isPhone"
          v-model="user.phone"
          placeholder="請輸入電話"
          :class="{
            'is-invalid': errors['phone'],
            'is-valid': !errors['phone'] && user.phone,
          }"
        ></VField>
        <!-- 注意：上方的rules因為要與methods自訂規則綁定故要加上bind -->
        <error-message name="phone" class="invalid-feedback"></error-message>
      </div>

      <div class="mb-3">
        <VField
          id="region"
          name="地區"
          class="form-control"
          as="select"
          rules="required"
          v-model="user.area"
          :class="{ 'is-invalid': errors['地區'] }"
        >
          <option value="">請選擇地區</option>
          <option value="台北市">台北市</option>
          <option value="高雄市">高雄市</option>
        </VField>
        <error-message name="地區" class="invalid-feedback"></error-message>
      </div>

      <div class="mb-3">
        <VField
          id="address"
          name="地址"
          type="text"
          class="form-control"
          rules="required"
          v-model="user.address"
          :class="{ 'is-invalid': errors['地址'] }"
          placeholder="請輸入地址"
        ></VField>
        <error-message name="地址" class="invalid-feedback"></error-message>
      </div>
      <!--注意：因Veevalidate是透過submit事件啟動驗證功能，如這裡再加上click事件則會導致功能失效-->
      <button class="btn btn-primary" type="submit">Submit</button>
    </VForm>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue';

export default {
  name: 'HomeView',
  components: {
    HelloWorld,
  },
  data() {
    return {
      user: {},
    };
  },
  methods: {
    onSubmit() {
      console.log(this.user);
    },
    isPhone(value) {
      const phoneNumber = /^(09)[0-9]{8}$/;
      return phoneNumber.test(value) ? true : '需要正確的電話號碼';
    },
  },
  created() {
    console.log(this);
  },
};
</script>
