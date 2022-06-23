<template>
  <div class="form">
    <div class="form-content">

      <div v-show="isLoginPage">
        <div
          class="field-content"
          v-for="field in loginFields"
          :key="field.header"
          v-show="field.id === logInStep"
        >
          <div class="field-header">{{ field.header }}</div>
          <div
            class="field-container"
          >
            <input
              class="field"
              :placeholder="field.placeholder"
              spellcheck="false"
              :type="field.type"
            />
          </div>
        </div>
      </div>

      <div v-show="!isLoginPage">
        <div
          class="field-content"
          v-for="field in signUpFields"
          :key="field.header"
          v-show="field.id === signUpStep"
        >
          <div class="field-header">{{ field.header }}</div>
          <div class="field-container">
            <input
              class="field"
              :placeholder="field.placeholder"
              spellcheck="false"
              autocomplete="off"
              :type="field.type"
            />
          </div>
        </div>
      </div>

      <div class="actions">
        <div
          class="back-button"
          @click="nextStep(true)"
          :style="{'background' : disableBackButton ? '#afa4a4' : '',
                    'color' : disableBackButton ? 'gray' : ''}"
        >
          Back
        </div>
        <div class="action-button" @click="nextStep(false)">Next</div>
      </div>
    </div>

    <div class="switchers">
      <div
        class="switcher"
        @click="isLoginPage = true"
        :style="{ 'border-color' : isLoginPage ? 'white' : 'transparent'}"
      >
        Login
      </div>

      <div class="text-white font-bold px-3 inline-block">|</div>

      <div
        class="switcher"
        @click="isLoginPage = false"
        :style="{ 'border-color' : !isLoginPage ? 'white' : 'transparent'}"
      >
        SignUp
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "authForm",
  data() {
    return {
      isLoginPage: true,
      logInStep: 0,
      signUpStep: 0,
      loginFields: [
        {
          id: 0,
          header: "Username",
          placeholder: "somebody.cool",
          type: "text"
        },
        {
          id: 1,
          header: "Password",
          placeholder: "qwerty1234",
          type: "password"
        }],
      signUpFields: [
        {
          id: 0,
          header: "Username",
          placeholder: "somebody.cool",
          type: "text"
        },
        {
          id: 1,
          header: "Email",
          placeholder: "youremail@gmail.com",
          type: "email"
        },
        {
          id: 2,
          header: "Password",
          placeholder: "qwerty1234",
          type: "password"
        },
        {
          id: 3,
          header: "Password again",
          placeholder: "qwerty1234",
          type: "password"
        }]
    }
  },
  computed: {
    disableBackButton() {
      if (this.isLoginPage) {
        return this.logInStep === 0
      }
      else {
        return this.signUpStep === 0
      }
    }
  },
  methods: {
    nextStep(reverse) {

      if (this.isLoginPage) {
        if (this.logInStep === this.loginFields.length - 1 && !reverse
          ||
          (reverse && this.logInStep === 0)) {
          return
        }

        this.logInStep += (reverse ? -1 : 1)
      } else {
        if (this.signUpStep === this.signUpFields.length - 1 && !reverse
          ||
          (this.signUpStep === 0 && reverse)
        ) {
          return
        }

        this.signUpStep += (reverse ? -1 : 1)
      }

    }
  }
}
</script>

<style scoped>

.form {
  font-family: 'Ubuntu', sans-serif;
  background: url("https://i.gifer.com/hyE.gif") center;
  @apply h-[550px] w-[350px] rounded-md mx-auto bg-black;
  @apply pt-3;
}

.form-content {
  @apply w-4/5 mx-auto h-[490px];
}

.field-container {
  @apply w-full rounded-md px-2 py-1 bg-white ;
}

.field-header {
  /*color : #afa4a4;*/
  @apply text-white font-bold
}

.field {
  @apply w-full outline-none
}

.switchers {
  @apply w-fit mx-auto text-white font-bold;
}

.switcher {
  @apply inline-block cursor-pointer px-2 py-1 border-2 border-transparent;
  @apply rounded-md;
}

.switcher:hover {
  @apply underline
}

.actions {
  @apply w-fit float-right;
}

.back-button {
  @apply px-3 py-1 rounded-md font-bold text-white;
  @apply cursor-pointer w-fit mt-2 bg-blue-300 inline-block;
}

.action-button {
  @apply px-3 py-1 rounded-md bg-blue-600 font-bold text-white;
  @apply cursor-pointer w-fit mt-2 inline-block;
}

</style>
