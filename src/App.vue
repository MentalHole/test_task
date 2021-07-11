<template>
  <div class="root">
    <form class="root">
      <div class="container">
        <h2 class="heading">Форма создания клиента</h2>
        <div class="field">
          <label class="field__label">
            Фамилия
            <span class="field__required">*</span>
          </label>
          <div class="field__group">
            <input
              v-model.trim="$v.form.lastname.$model"
              class="field__input"
              :class="$v.form.lastname.$error ? 'is-invalid' : ''"
              type="text"
              placeholder="Иванов"
            />
            <small
              class="invalid--message"
              v-if="$v.form.lastname.$dirty && !$v.form.lastname.required"
              >Поле обязательно для заполнения</small
            >
            <small class="invalid--message" v-if="!$v.form.lastname.minLength"
              >Должно быть не менее 3 знаков</small
            >
            <small class="invalid--message" v-if="!$v.form.lastname.maxLength"
              >Максимум знаков 12</small
            >
          </div>
        </div>
        <div class="field">
          <label class="field__label"
            >Имя
            <span class="field__required">*</span>
          </label>
          <div class="field__group">
            <input
              v-model.trim="$v.form.firstname.$model"
              class="field__input"
              :class="$v.form.firstname.$error ? 'is-invalid' : ''"
              type="text"
              placeholder="Иван"
            />
            <small
              class="invalid--message"
              v-if="$v.form.firstname.$dirty && !$v.form.firstname.required"
              >Поле обязательно для заполнения</small
            >
            <small class="invalid--message" v-if="!$v.form.firstname.minLength"
              >Должно быть не менее 3 знаков</small
            >
            <small class="invalid--message" v-if="!$v.form.firstname.maxLength"
              >Максимум знаков 12</small
            >
          </div>
        </div>
        <div class="field">
          <label class="field__label">Отчество</label>
          <div class="field__group">
            <input
              class="field__input"
              :class="$v.form.patronymic.$error ? 'is-invalid' : ''"
              type="text"
              placeholder="Иванович"
              v-model="form.patronymic"
            />
            <small class="invalid--message" v-if="!$v.form.patronymic.minLength"
              >Должно быть не менее 3 знаков</small
            >
            <small class="invalid--message" v-if="!$v.form.patronymic.maxLength"
              >Максимум знаков 12</small
            >
          </div>
        </div>
        <div class="field">
          <label class="field__label"
            >Дата рождения
            <span class="field__required">*</span>
          </label>
          <div class="field__group">
            <input
              class="field__input"
              :class="!$v.form.birthdate.required ? 'is-invalid' : ''"
              type="date"
              v-model="$v.form.birthdate.$model"
            />
            <small
              class="invalid--message"
              v-if="$v.form.birthdate.$dirty && !$v.form.birthdate.required"
              >Поле обязательно для заполнения</small
            >
          </div>
        </div>
        <div class="field">
          <label class="field__label"
            >Номер телефона
            <span class="field__required">*</span>
          </label>
          <div class="field__group">
            <input
              class="field__input"
              :class="$v.form.phonenumber.$error ? 'is-invalid' : ''"
              v-model="$v.form.phonenumber.$model"
              placeholder="77771234567"
            />
            <small
              class="invalid--message"
              v-if="!$v.form.phonenumber.required && $v.form.phonenumber.$dirty"
              >Поле обязательно для заполнения</small
            >
            <small
              class="invalid--message"
              v-if="!$v.form.phonenumber.numeric && $v.form.phonenumber.$dirty"
              >Введите цифры</small
            >
          </div>
        </div>
        <div class="field">
          <label class="field__label">Пол</label>
          <div class="field__gender">
            <div class="field__group">
              <label for="male">Мужской</label>
              <input
                id="gender"
                class="field__input"
                type="radio"
                value="male"
                v-model="form.gender"
              />
            </div>
            <div class="field__group">
              <label for="female">Женский</label>
              <input
                id="gender2"
                class="field__input"
                type="radio"
                value="female"
                v-model="form.gender"
              />
            </div>
          </div>
          <div class="field__group"></div>
        </div>
        <div class="field">
          <label class="field__label"
            >Группа клиентов
            <span class="field__required">*</span>
          </label>
          <div class="field__group">
            <select
              class="field__input"
              :class="$v.form.selectedClientGroups.$error ? 'is-invalid' : ''"
              v-model="form.selectedClientGroups"
              size="4"
              multiple
            >
              <option disabled>Можно выбрать несколько</option>
              <option value="VIP">VIP</option>
              <option value="Проблемные">Проблемные</option>
              <option value="ОМС">ОМС</option>
            </select>
            <small
              class="invalid--message"
              v-if="
                $v.form.selectedClientGroups.$dirty &&
                !$v.form.selectedClientGroups.required
              "
              >Выберите хотя бы одну группу</small
            >
          </div>
        </div>
        <div class="field">
          <label class="field__label">Лечащий врач</label>
          <div class="field__group">
            <select class="field__input" v-model.trim="form.selectedDoctor">
              <option disabled>Выберите одного</option>
              <option v-for="(doctor, index) in form.doctors" :key="index">
                {{ doctor.name }}
              </option>
            </select>
          </div>
        </div>
        <div class="field">
          <div class="field__group">
            <label class="field__label"
              >Не отправлять СМС
              <input
                class="field__input"
                type="checkbox"
                v-model="form.dontSendSms"
              />
            </label>
          </div>
        </div>
      </div>

      <!-- Adress -->
      <div class="container">
        <h2 class="heading">Адрес</h2>
        <div class="field">
          <label class="field__label">Индекс</label>
          <div class="field__group">
            <input
              class="field__input"
              :class="$v.form.houseIndex.$error ? 'is-invalid' : ''"
              v-model="form.houseIndex"
            />
            <small class="invalid--message" v-if="!$v.form.houseIndex.numeric"
              >Должны быть цифры</small
            >
          </div>
        </div>
        <div class="field">
          <label class="field__label">Страна</label>
          <div class="field__group">
            <input
              type="text"
              class="field__input"
              :class="$v.form.country.$error ? 'is-invalid' : ''"
              v-model="form.country"
            />
          </div>
        </div>
        <div class="field">
          <label class="field__label">Область</label>
          <div class="field__group">
            <input
              type="text"
              class="field__input"
              :class="$v.form.firstname.$error ? 'is-invalid' : ''"
              v-model="form.region"
            />
          </div>
        </div>
        <div class="field">
          <label class="field__label"
            >Город
            <span class="field__required">*</span>
          </label>
          <div class="field__group">
            <input
              type="text"
              class="field__input"
              :class="$v.form.city.$error ? 'is-invalid' : ''"
              v-model.trim="$v.form.city.$model"
            />
            <small
              class="invalid--message"
              v-if="$v.form.city.$dirty && !$v.form.city.required"
              >Поле обязательно</small
            >
            <small class="invalid--message" v-if="!$v.form.city.minLength"
              >Минимум 3 буквы</small
            >
            <small class="invalid--message" v-if="!$v.form.city.maxLength"
              >Максимум 18 букв</small
            >
          </div>
        </div>
        <div class="field">
          <label class="field__label">Улица</label>
          <div class="field__group">
            <input
              type="text"
              class="field__input"
              :class="$v.form.street.$error ? 'is-invalid' : ''"
              v-model="form.street"
            />
          </div>
        </div>
        <div class="field">
          <label class="field__label">Дом</label>
          <div class="field__group">
            <input
              type="text"
              class="field__input"
              :class="$v.form.house.$error ? 'is-invalid' : ''"
              v-model="form.house"
            />
          </div>
        </div>

        <!-- Passport -->
        <h2 class="heading">Паспорт</h2>
        <div class="field">
          <label class="field__label"
            >Тип документа
            <span class="field__required">*</span>
          </label>
          <div class="field__group">
            <select
              type="text"
              class="field__input"
              :class="$v.form.documentType.$error ? 'is-invalid' : ''"
              v-model="form.documentType"
            >
              <option value="Паспорт">Паспорт</option>
              <option value="Свидетельство о рождении">
                Свидетельство о рождении
              </option>
              <option value="Вод. удостоверение">Вод. удостоверение</option>
            </select>
            <small
              class="invalid--message"
              v-if="
                !$v.form.documentType.required && $v.form.documentType.$dirty
              "
              >Поле обязательно для заполнения</small
            >
          </div>
        </div>

        <div class="field">
          <label class="field__label">Серия</label>
          <div class="field__group">
            <input type="text" class="field__input" />
          </div>
        </div>

        <div class="field">
          <label class="field__label">Номер</label>
          <div class="field__group">
            <input type="text" class="field__input" />
          </div>
        </div>

        <div class="field">
          <label class="field__label">Кем выдан</label>
          <div class="field__group">
            <input type="text" class="field__input" />
          </div>
        </div>

        <div class="field">
          <label class="field__label"
            >Дата выдачи
            <span class="field__required">*</span>
          </label>
          <div class="field__group">
            <input
              type="date"
              class="field__input"
              :class="!$v.form.issueDate.required ? 'is-invalid' : ''"
              v-model="$v.form.issueDate.$model"
            />
            <small
              class="invalid--message"
              v-if="!$v.form.issueDate.required && $v.form.issueDate.$dirty"
              >Поле обязательно для заполнения</small
            >
          </div>
        </div>
        <button class="btn" @click.prevent="submit">Отправить</button>
      </div>
    </form>
    <div id="modal" class="modal" :class="modalVisible ? 'show-modal' : ''">
      <div class="modal-content">
        <p class="typo__p" v-if="submitStatus === 'OK'">
          Форма успешно отправлена!
        </p>
        <p class="typo__p" v-if="submitStatus === 'ERROR'">
          Пожалуйста, заполните форму правильно!
        </p>
        <p class="typo__p" v-if="submitStatus === 'PENDING'">Отправка...</p>
        <button class="btn" @click="modalVisible = false">Принято</button>
      </div>
    </div>
  </div>
</template>

<script>
import {
  required,
  minLength,
  maxLength,
  numeric,
} from "vuelidate/lib/validators";

export default {
  data() {
    return {
      submitStatus: null,
      modalVisible: false,
      form: {
        firstname: "",
        lastname: "",
        patronymic: "",
        birthdate: null,
        selectedDoctor: [],
        doctors: [
          {
            name: "Иванов",
          },
          {
            name: "Захаров",
          },
          {
            name: "Чернышев",
          },
        ],
        phonenumber: null,
        gender: [],
        selectedClientGroups: [],
        clientgroups: [
          {
            title: "VIP",
          },
          {
            title: "Проблемные",
          },
          {
            title: "ОМС",
          },
        ],
        dontSendSms: false,

        houseIndex: null,
        city: "",
        documentType: "",
        issueDate: null,
      },
    };
  },
  validations: {
    form: {
      firstname: {
        required,
        minLength: minLength(3),
        maxLength: maxLength(10),
      },
      lastname: {
        required,
        minLength: minLength(3),
        maxLength: maxLength(10),
      },
      patronymic: {
        minLength: minLength(3),
        maxLength: maxLength(12),
      },
      phonenumber: {
        required,
        numeric,
      },
      selectedClientGroups: {
        required,
      },
      birthdate: {
        required,
      },
      houseIndex: {
        numeric,
      },
      country: {
        minLength: minLength(3),
      },
      street: {
        minLength: minLength(3),
      },
      house: { numeric },
      city: {
        required,
        minLength: minLength(3),
        maxLength: maxLength(16),
      },
      documentType: {
        required,
      },
      issueDate: {
        required,
      },
    },
  },
  methods: {
    submit() {
      this.$v.form.$touch();
      this.modalVisible = true;
      if (this.$v.form.$invalid) {
        this.submitStatus = "ERROR";
      } else {
        this.submitStatus = "PENDING";
        setTimeout(() => {
          this.submitStatus = "OK";
        }, 500);
      }
    },
  },
};
</script>

<style lang="scss">
@import "/scss/style.scss";
</style>