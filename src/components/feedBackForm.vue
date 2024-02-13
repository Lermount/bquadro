<template>
    <div class="modal">
        <div class="modal-content">
            <button type="button" class="btn-close ms-auto" @click="closeModal"></button>
            <h3 v-if="thanks" class="h3">Форма успешно отправлена</h3>
            <form v-else @submit.prevent="submitForm">
                <div class="mb-3">
                    <label for="name" class="form-label">Имя:</label>
                    <input type="text" placeholder="Иванов Иван Иванович" class="form-control" id="name"
                        v-model="formData.name" required>
                </div>
                <div class="mb-3">
                    <label for="phone" class="form-label">Телефон:</label>
                    <input type="tel" placeholder="+79991112233" pattern="^\+?\d{11}$" class="form-control" id="phone"
                        v-model="formData.phone" required>
                </div>
                <div class="mb-3">
                    <label for="email" class="form-label">Email:</label>
                    <input type="email" placeholder="example@mail.ru" class="form-control" id="email"
                        v-model="formData.email" required>
                </div>
                <div class="mb-3">
                    <label for="file" class="form-label">Прикрепить файл:</label>
                    <input type="file" class="form-control" id="file" @change="handleFileUpload"
                        accept=".jpg, .jpeg, .png, .pdf" required>
                </div>

                <div class="mb-3 form-check">
                    <input type="checkbox" class="form-check-input" id="consent" v-model="formData.consent" required>
                    <label for="consent" class="form-check-label">Согласие на обработку персональных данных</label>
                </div>
                <div>
                    <button :disabled="!formData.consent" type="submit" class="btn btn-primary">Отправить</button>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            formData: {
                name: "",
                phone: "",
                email: "",
                file: null,
                consent: false,
            },

            thanks: false
        };
    },

    methods: {
        handleFileUpload(event) {
            const file = event.target.files[0];

            // Проверьте размер файла
            if (file && file.size > 2e6) {
                alert("Максимальный размер файла - 2 МБ");
                this.formData.file = null;
            } else {
                this.formData.file = file;
            }
        },

        submitForm() {
            // Отправка данных формы на сервер
            console.log(this.formData);
            // Сброс данных формы
            this.formData = {
                name: "",
                phone: "",
                email: "",
                file: null,
                consent: false,
            };
            this.thanks = !this.thanks
        },

        closeModal() {
            this.$emit('close-modal', false);
        }
    },
}
</script>
<style scoped>
.modal {
    display: block;
    position: relative;
}

.modal::before {
    content: "";
    background: #000;
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    opacity: 0.7;
    z-index: 9999;
}

.modal-content {
    z-index: 99999;
    padding: 20px;
    position: fixed;
    top: 20%;
    left: 0;
    right: 0;
    width: 50%;
    margin: 0 auto;
}
</style>