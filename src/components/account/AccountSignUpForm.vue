<template lang="">
    <div class="grey lighten-5" style="font-family: 'Noto Sans KR', sans-serif">
        <v-container class="white">
            <v-row justify="center">
                <v-col cols="auto" style="padding-bottom: 90px">
                    <router-link to="/">
                        <v-img
                            :src="require('@/assets/logo.png')"
                            width="120"
                            class="mx-auto mb-6"></v-img>
                    </router-link>
                    <v-card width="460">
                        <v-card-text class="text-center px-12 py-16">
                            <v-form @submit.prevent="onSubmit" ref="form">
                                <div class="text-h4 font-weight-black mb-10">회원 신청하기</div>
                                <div class="d-flex">
                                    <v-text-field
                                        v-model="email"
                                        label="이메일"
                                        :rules="email_rule"
                                        :disabled="false"
                                        required>
                                    </v-text-field>
                                    <v-btn text large outlined style="font-size: 13px"
                                            class="mt-3 ml-5" color="teal lighten-1"
                                            @click="checkDuplicateEmail"
                                            :disabled="email == ''">
                                        이메일 <br/>중복 확인
                                    </v-btn>
                                </div>

                                <v-btn type="submit" block x-large rounded
                                        color="orange lighten-1" class="mt-6"
                                        :disabled="emailPass == false">회원 신청하기</v-btn>
                                <v-btn type="submit" block x-large rounded
                                        color="orange lighten-1" class="mt-6"
                                        :disabled="emailPass == false">가입 취소하기</v-btn>
                            </v-form>
                        </v-card-text>
                    </v-card>
                </v-col>
            </v-row>
        </v-container>
    </div>
</template>

<script>
export default {
    data () {
        return {
            email: "",
            emailPass: false,
            email_rule: [
                v => !!v || '이메일을 입력해주세요!',
                v => {
                    const replaceV = v.replace(/(\s*)/g, '')
                    const pattern = /^[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*.[a-zA-Z]{2,3}$/
                    return pattern.test(replaceV) || '올바른 이메일 형식으로 입력해주세요!'
                }
            ]
        }
    },
    methods: {
        onSubmit () {
            if (this.$refs.form.validate()) {
                const { email } = this
                this.$emit("submit", { email })
            } else {
                alert('올바른 정보를 입력하세요!')
            }
            if (!this.emailPass) {
                alert("이메일 중복 확인을 해주세요!")
            }
        }
    }
}
</script>

<style lang="">
    
</style>