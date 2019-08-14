<template>
    <v-container fill-height>
        <v-layout align-center justify-center>
            <v-flex xs10 sm8 md7 lg5>
                <v-card class="pa-3 elevation-8">
                    <v-form @submit="formSubmitt" ref="form">
                        <v-card-title class="my-4">Форма обратной связи</v-card-title>
                        <v-card-text>
                            <v-text-field label="Имя" name="name" v-model="name" outlined />
                            <v-text-field
                                label="Телефон"
                                name="tel"
                                v-model="tel"
                                outlined
                                v-mask="'+7 (##) ## ## ###'"
                                :rules="[requiredRule, telRule]"
                            />
                            <v-checkbox
                                v-model="accept"
                                label="Согласен на обработку пользовательских данных"
                                :rules="[requiredRule]"
                            />
                        </v-card-text>
                        <v-card-actions>
                            <v-spacer />
                            <v-btn
                                type="submit"
                                text
                                color="primary"
                                :disabled="!isValidForm"
                            >Отправить</v-btn>
                        </v-card-actions>
                    </v-form>
                </v-card>
            </v-flex>
        </v-layout>
    </v-container>
</template>

<script>
import { mask } from "vue-the-mask";

export default {
    directives: {
        mask
    },
    data() {
        return {
            name: "",
            tel: "",
            accept: true,
            isValidForm: false,
            requiredRule: value => !!value || "Обязательное поле",
            telRule: value => value.length > 16 || "Заполните поле полностью"
        };
    },
    methods: {
        formValidate() {
            this.isValidForm = this.$refs.form.validate();
        },
        formSubmitt(e) {
            e.preventDefault();
            console.log(e);
        }
    },
    watch: {
        tel(value) {
            this.formValidate();
        },
        accept(value) {
            this.formValidate();
        }
    }
};
</script>
