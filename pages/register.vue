<template>
    <div>
    <loading :active.sync="isLoading" :color="color" :background-color="backgroundColor"> </loading>
    <div class="container auth is-fluid px-0">
        <div class="columns is-multiline is-gapless">
            <div class="column is-6-tablet is-5-desktop is-5-widescreen is-5-fullhd">
                <div class="auth has-background-primary">
                    <div class="auth-content">
                        <div class="has-text-centered">
                            <img src="~assets/images/logo1.svg" alt="" width="300px">
                        </div>
                        <div class="auth-inner-content my-6">
                            <div class="has-text-white has-text-weight-regular is-flex ai--fs mb-5">
                                <img src="~assets/images/bcheckmark.webp" alt="" class="bullet mt-1 mr-3">
                                Family Tree 365 is a secure online website
                                which you can use to create your own family tree(s) with.</div>
                            <div class="has-text-white has-text-weight-regular is-flex ai--fs mb-5">
                                <img src="~assets/images/bcheckmark.webp" alt="" class="bullet mt-1 mr-3">
                                It has a tree viewer and DNA support
                                more features are planned such as the inclusion of archive databases and
                                collections</div>
                            <div class="has-text-white has-text-weight-regular is-flex ai--fs">
                                <img src="~assets/images/bcheckmark.webp" alt="" class="bullet mt-1 mr-3">
                              Set up your first family tree free of charge.
                              We offer different pricing levels with optional subscriptions if you need to create extra trees.</div>
                        </div>
                        <img class="auth-img" src="~assets/images/mockup03@2x.webp" alt="">
                    </div>
                </div>
            </div>
            <form @submit.prevent="register()" class="column is-6-tablet is-7-desktop is-7-widescreen is-7-fullhd is-gapless is-flex ai--c">

                <div class="auth-form is-gapless">
                    <div class="mb-5">
                        <NuxtLink to="/" class="is-size-6 is-flex has-text-link has-text-weight-medium mb-2">
                            <font-awesome-icon :icon="['fas', 'angle-left']" class="mt-1 mr-2" />Back to Home</NuxtLink>
                        <h1 class="is-size-4 has-text-black has-text-weight-bold">
                            Create your account
                        </h1>
                    </div>
                    <div v-if="error" class="notification is-danger">
                        {{ message }}
                    </div>
                    <div v-for="error in errors" class="notification is-danger">
                        {{ error[0] }}
                    </div>
                    <div class="mb-5">
                        <div class="columns">
                            <div class="column">
                                <div class="field">
                                    <p class="control has-icons-left has-icons-right">
                                        <input class="input is-large" type="text" placeholder="First name" :class="{ 'is-danger': $v.registration.first_name.$error }" v-model="registration.first_name">
                                        <span class="icon is-small is-left">
                                            <font-awesome-icon :icon="['fas', 'user']"/>
                                        </span>
                                    </p>
                                    <p class="help" :class="{ 'is-danger': $v.registration.first_name.$error }" v-if="!$v.registration.first_name.required">Field is required</p>
                                </div>
                            </div>
                            <div class="column">
                                <div class="field">
                                    <p class="control has-icons-left has-icons-right">
                                        <input class="input is-large" type="text" :class="{ 'is-danger': $v.registration.last_name.$error }" placeholder="Last name" v-model="registration.last_name">
                                        <span class="icon is-small is-left">
                                            <font-awesome-icon :icon="['fas', 'user']"/>
                                        </span>
                                    </p>
                                    <p class="help" :class="{ 'is-danger': $v.registration.last_name.$error }" v-if="!$v.registration.last_name.required">Field is required</p>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="mb-5">
                        <div class="field">
                            <p class="control has-icons-left has-icons-right">
                                <input class="input is-large" type="email" placeholder="Email address" :class="{ 'is-danger': $v.registration.email.$error }" v-model="registration.email">
                                <span class="icon is-small is-left">
                                    <font-awesome-icon :icon="['fas', 'envelope']"/>
                                </span>
                            </p>
                            <p class="help" :class="{ 'is-danger': $v.registration.email.$error }" v-if="!$v.registration.email.required">Field is required</p>
                        </div>
                    </div>
                    <div class="mb-5">
                        <div class="field">
                            <p class="control has-icons-left has-icons-right">
                                <input class="input is-large" type="password" placeholder="Password" :class="{ 'is-danger': $v.registration.password.$error }" v-model="registration.password">
                                <span class="icon is-small is-left">
                                    <font-awesome-icon :icon="['fas', 'lock']"/>
                                </span>
                            </p>
                            <p class="help" :class="{ 'is-danger': $v.registration.password.$error }" v-if="!$v.registration.password.required">Field is required</p>
                        </div>
                    </div>
                    <div class="mb-5">
                        <div class="field">
                            <p class="control has-icons-left has-icons-right">
                                <input class="input is-large" type="password" placeholder="Confirm Password" :class="{ 'is-danger': $v.registration.password_confirmation.$error }" v-model="registration.password_confirmation">
                                <span class="icon is-small is-left">
                                    <font-awesome-icon :icon="['fas', 'lock']"/>
                                </span>
                            </p>
                            <p class="help" :class="{ 'is-danger': $v.registration.password_confirmation.$error }" v-if="!$v.registration.password_confirmation.required">Field is required</p>
                        </div>
                    </div>
                    <div class="mb-5">
                        <div class="columns is-mobile is-gapless">
                            <div class="column">
                                <label class="checkbox">
                                    <input type="checkbox" v-model="registration.conditions_terms">
                                    Agree to <NuxtLink to="/termsandconditions" class="has-text-link has-text-weight-medium">terms and
                                        conditions</NuxtLink>
                                </label>
                                <p class="help" :class="{ 'is-danger': $v.registration.conditions_terms.$error }" v-if="!$v.registration.conditions_terms.checked">Field is required</p>
                            </div>
                        </div>

                    </div>
                    <div class="mb-6">
                        <button
                            class="button theme-button theme-button-xl has-background-primary is-uppercase has-text-weight-medium has-text-white">
                            register
                        </button>
                    </div>
                    <div>
                        <p class="is-size-6 has-text-dark has-text-centered has-text-weight-regular">
                            Already have an account?<NuxtLink to="/login" class="has-text-link has-text-weight-medium">
                                Sign in </NuxtLink>
                        </p>
                    </div>
                </div>

            </form>
        </div>
    </div>
    </div>
</template>

<script>
import { required } from 'vuelidate/lib/validators'
import Loading from 'vue-loading-overlay';
import 'vue-loading-overlay/dist/vue-loading.css';
export default {
    middleware: 'guest',
    components: {
        Loading
    },
    data() {
        return {
            error: false,
            message: "",
            errors:null,
            isLoading: false,
            fullPage: true,
            color: '#4fcf8d',
            backgroundColor: '#ffffff',
            registration: {
                first_name: "",
                last_name: "",
                email: "",
                password: "",
                password_confirmation: '',
                conditions_terms: false,
            }
        };
    },
    validations: {
            registration: {
                first_name: {
                    required,
                },
                last_name: {
                    required,
                },
                email: {
                    required,
                },
                password: {
                    required,
                },
                password_confirmation: {
                    required,
                },
                conditions_terms: {
                    checked: value => value === true,
                }
            },
    },
    methods: {
        async register() {
            this.$v.$touch();

            if (this.$v.$invalid) {
                console.log("fail")

                return -1
            }

            try {
                this.isLoading = true

                const response = await this.$axios
                  .$post("/api/register", this.registration);

                this.$router.push("/login");
                this.isLoading = false;
            } catch (error) {
              this.isLoading = false
              this.error = true;
              this.message = error.response.data.message;
              this.errors =  error.response.data.errors;
            }

        }
    }
}
</script>

 <style scoped>
    @import '~/assets/css/base.css';
</style>
