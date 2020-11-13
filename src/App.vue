<template>
  <div id="app">
    <div class="container">
      <h1>Регистрация</h1>
      <div class="card">
        <div>
          <h2 class="form__title">Основная информация</h2>
          <div class="form__grid form__grid--3">
            <div
              class="form__group"
              :class="{
                'form__group--error': $v.surname.$error,
                'form__group--success':
                  !$v.surname.$error && $v.surname.$model !== '',
              }"
            >
              <input
                class="form__input form__input--text"
                type="text"
                placeholder="Фамилия*"
                v-model="$v.surname.$model"
              />
              <div class="form__error-message" v-if="$v.surname.$error">
                Это обязательное поле
              </div>
            </div>
            <div
              class="form__group "
              :class="{
                'form__group--error': $v.name.$error,
                'form__group--success':
                  !$v.name.$error && $v.name.$model !== '',
              }"
            >
              <input
                class=" form__input form__input--text"
                type="text"
                placeholder="Имя*"
                v-model.trim="$v.name.$model"
              />
              <div class="form__error-message" v-if="$v.name.$error">
                Это обязательное поле
              </div>
            </div>
            <div
              class="form__group"
              :class="{ 'form__group--success': patronymic !== '' }"
            >
              <input
                class="form__input form__input--text"
                type="text"
                v-model.trim="patronymic"
                placeholder="Отчество"
              />
            </div>
          </div>
          <div class="form__grid form__grid--2">
            <div
              class="form__group"
              :class="{
                'form__group--error': $v.dateOfBirth.$error,
                'form__group--success':
                  !$v.dateOfBirth.$error && $v.dateOfBirth.$model !== '',
              }"
            >
              <input
                class="form__input form__input--text"
                type="text"
                placeholder="Дaта рождения*"
                v-model="$v.dateOfBirth.$model"
              />
              <div class="form__error-message" v-if="$v.dateOfBirth.$error">
                Это обязательное поле
              </div>
            </div>
            <div
              class="form__group"
              :class="{
                'form__group--error': $v.tel.$error,
                'form__group--success': !$v.tel.$error && $v.tel.$model !== '',
              }"
            >
              <input
                class="form__input form__input--text"
                type="tel"
                placeholder="Номер телефона*"
                v-model="$v.tel.$model"
                maxlength="11"
                show-word-limit
              />
              <span class="form__counter"
                >{{ $v.tel.$model.length }}/{{
                  $v.tel.$params.maxLength.max
                }}</span
              >
              <div class="form__error-message" v-if="$v.tel.$error">
                Номер должен быть от 7 до 11 цифр
              </div>
            </div>

            <div
              class="form__group"
              :class="{
                'form__group--error': $v.customerGroup.$error,
                'form__group--success':
                  !$v.customerGroup.$error && customerGroup.length,
              }"
            >
              <div
                class="form__input"
                :class="{ 'form__input-light': !customerGroup.length }"
                @click="openMenu('form__customer-group')"
              >
                <div v-if="customerGroup.length">
                  <span v-for="(item, index) in customerGroup" :key="index">
                    {{ item }}
                  </span>
                </div>
                <div v-else>Группа клиентов*</div>
                <span class="form__arrow"
                  ><svg
                    width="1.3em"
                    height="1.3em"
                    viewBox="0 0 16 16"
                    class="bi bi-caret-down"
                    fill="currentColor"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                    <path
                      fill-rule="evenodd"
                      d="M3.204 5L8 10.481 12.796 5H3.204zm-.753.659l4.796 5.48a1 1 0 0 0 1.506 0l4.796-5.48c.566-.647.106-1.659-.753-1.659H3.204a1 1 0 0 0-.753 1.659z"
                    /></svg
                ></span>
              </div>
              <div class="form__menu" id="form__customer-group">
                <div @click="updateCustomerGroup('VIP')">
                  <input
                    class="form__input--checkbox"
                    type="checkbox"
                    :checked="customerGroup.find((i) => i === 'VIP')"
                  />VIP
                </div>
                <div @click="updateCustomerGroup('Проблемные')">
                  <input
                    class="form__input--checkbox"
                    type="checkbox"
                    :checked="customerGroup.find((i) => i === 'Проблемные')"
                  />Проблемные
                </div>
                <div @click="updateCustomerGroup('ОМС')">
                  <input
                    class="form__input--checkbox"
                    type="checkbox"
                    :checked="customerGroup.find((i) => i === 'ОМС')"
                  />ОМС
                </div>
              </div>
            </div>

            <div
              class="form__group"
              :class="{ 'form__group--success': doctor !== '' }"
            >
              <div
                class="form__input"
                :class="{ 'form__input-light': doctor === '' }"
                @click="openMenu('form__doctor')"
              >
                {{ doctor === "" ? "Лечащий врач" : doctor }}
                <span class="form__arrow"
                  ><svg
                    width="1.3em"
                    height="1.3em"
                    viewBox="0 0 16 16"
                    class="bi bi-caret-down"
                    fill="currentColor"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                    <path
                      fill-rule="evenodd"
                      d="M3.204 5L8 10.481 12.796 5H3.204zm-.753.659l4.796 5.48a1 1 0 0 0 1.506 0l4.796-5.48c.566-.647.106-1.659-.753-1.659H3.204a1 1 0 0 0-.753 1.659z"
                    /></svg
                ></span>
              </div>
              <div class="form__menu" id="form__doctor">
                <div
                  :class="{ active: doctor === 'Иванов' }"
                  @click="doctor = 'Иванов'"
                >
                  Иванов
                </div>
                <div
                  :class="{ active: doctor === 'Захаров' }"
                  @click="doctor = 'Захаров'"
                >
                  Захаров
                </div>
                <div
                  :class="{ active: doctor === 'Чернышева' }"
                  @click="doctor = 'Чернышева'"
                >
                  Чернышева
                </div>
              </div>
            </div>
            <div class="form__group form__group--radio">
              <div>Пол</div>
              <div>
                <div>
                  <input
                    class="form__input--radio"
                    type="radio"
                    id="form__gender-1"
                    name="gender"
                  />
                  <label for="form__gender-1">Мужской</label>
                </div>
                <div>
                  <input
                    class="form__input--radio"
                    type="radio"
                    id="form__gender-2"
                    name="gender"
                  />
                  <label for="form__gender-2">Женский</label>
                </div>
              </div>
            </div>
            <div class="form__group form__group--checkbox">
              <input
                class="form__input--checkbox"
                type="checkbox"
                id="form__sms"
              />
              <label for="form__sms">Не отправлять СМС</label>
            </div>
          </div>
        </div>
      </div>
      <div class="card">
        <div>
          <h2 class="form__title">Адрес</h2>
          <div class="form__grid form__grid--2">
            <div
              class="form__group"
              :class="{ 'form__group--success': index !== '' }"
            >
              <input
                class="form__input"
                type="text"
                placeholder="Индекс"
                v-model="index"
              />
            </div>
            <div
              class="form__group"
              :class="{ 'form__group--success': country !== '' }"
            >
              <input
                class="form__input"
                type="text"
                placeholder="Страна"
                v-model="country"
              />
            </div>
            <div
              class="form__group"
              :class="{ 'form__group--success': region !== '' }"
            >
              <input
                class="form__input"
                type="text"
                placeholder="Область"
                v-model="region"
              />
            </div>
            <div
              class="form__group"
              :class="{
                'form__group--error': $v.city.$error,
                'form__group--success': !$v.city.$error && city !== '',
              }"
            >
              <input
                class="form__input"
                type="text"
                placeholder="Город*"
                v-model="$v.city.$model"
              />
              <div class="form__error-message" v-if="$v.city.$error">
                Это обязательное поле
              </div>
            </div>
            <div
              class="form__group"
              :class="{ 'form__group--success': street !== '' }"
            >
              <input
                class="form__input"
                type="text"
                placeholder="Улица"
                v-model="street"
              />
            </div>
            <div
              class="form__group"
              :class="{ 'form__group--success': home !== '' }"
            >
              <input
                class="form__input"
                type="text"
                placeholder="Дом"
                v-model="home"
              />
            </div>
          </div>
        </div>
      </div>
      <div class="card">
        <div>
          <h2 class="form__title">Паспортные данные</h2>
          <div class="form__grid form__grid--2">
            <div
              class="form__group"
              :class="{
                'form__group--error': $v.typeDocument.$error,
                'form__group--success':
                  !$v.typeDocument.$error && typeDocument !== '',
              }"
            >
              <div
                class="form__input"
                :class="{ 'form__input-light': $v.typeDocument.$model === '' }"
                @click="openMenu('form__type-document')"
              >
                {{ typeDocument === "" ? "Тип документа" : typeDocument }}
                <span class="form__arrow"
                  ><svg
                    width="1.3em"
                    height="1.3em"
                    viewBox="0 0 16 16"
                    class="bi bi-caret-down"
                    fill="currentColor"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                    <path
                      fill-rule="evenodd"
                      d="M3.204 5L8 10.481 12.796 5H3.204zm-.753.659l4.796 5.48a1 1 0 0 0 1.506 0l4.796-5.48c.566-.647.106-1.659-.753-1.659H3.204a1 1 0 0 0-.753 1.659z"
                    /></svg
                ></span>
                <div class="form__error-message" v-if="$v.typeDocument.$error">
                  Это обязательное поле
                </div>
              </div>
              <div class="form__menu" id="form__type-document">
                <div
                  :class="{ active: typeDocument === 'Паспорт' }"
                  @click="typeDocument = 'Паспорт'"
                >
                  Паспорт
                </div>
                <div
                  :class="{
                    active: typeDocument === 'Свидетельство о рождении',
                  }"
                  @click="typeDocument = 'Свидетельство о рождении'"
                >
                  Свидетельство о рождении
                </div>
                <div
                  :class="{ active: typeDocument === 'Вод. удостоверение' }"
                  @click="typeDocument = 'Вод. удостоверение'"
                >
                  Вод. удостоверение
                </div>
              </div>
            </div>
            <div
              class="form__group"
              :class="{ 'form__group--success': series !== '' }"
            >
              <input
                class="form__input"
                type="text"
                placeholder="Серия"
                v-model="series"
              />
            </div>
          </div>
          <div class="form__grid form__grid--3">
            <div
              class="form__group"
              :class="{ 'form__group--success': number !== '' }"
            >
              <input
                class="form__input"
                type="text"
                placeholder="Номер"
                v-model="number"
              />
            </div>
            <div
              class="form__group"
              :class="{ 'form__group--success': issuedBy !== '' }"
            >
              <input
                class="form__input"
                type="text"
                placeholder="Кем выдан"
                v-model="issuedBy"
              />
            </div>
            <div
              class="form__group"
              :class="{
                'form__group--error': $v.dateOfIssue.$error,
                'form__group--success':
                  !$v.dateOfIssue.$error && $v.dateOfIssue.$model !== '',
              }"
            >
              <input
                class="form__input"
                type="text"
                placeholder="Дата выдачи*"
                v-model="$v.dateOfIssue.$model"
              />
              <div class="form__error-message" v-if="$v.dateOfIssue.$error">
                Это обязательное поле
              </div>
            </div>
          </div>
        </div>
      </div>
      <button
        class="btn"
        :class="{ 'btn--disabled': $v.$invalid }"
        :disabled="$v.$invalid"
        @click="prepared"
      >
        Отправить
      </button>
      <div class="message">
        <div class="message__logo">
          <svg
            width="2em"
            height="2em"
            viewBox="0 0 16 16"
            class="bi bi-check"
            fill="currentColor"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              fill-rule="evenodd"
              d="M10.97 4.97a.75.75 0 0 1 1.071 1.05l-3.992 4.99a.75.75 0 0 1-1.08.02L4.324 8.384a.75.75 0 1 1 1.06-1.06l2.094 2.093 3.473-4.425a.236.236 0 0 1 .02-.022z"
            />
          </svg>
        </div>
        <div class="message__text">
          <h3>Готово</h3>
          <span>Вы успешно зарегестрировались</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { required, minLength, maxLength } from "vuelidate/lib/validators";

export default {
  name: "App",
  data: () => ({
    surname: "",
    name: "",
    patronymic: "",
    dateOfBirth: "",
    tel: "",
    customerGroup: [],
    doctor: "",
    index: "",
    country: "",
    region: "",
    city: "",
    street: "",
    home: "",
    typeDocument: "",
    series: "",
    number: "",
    issuedBy: "",
    dateOfIssue: "",
  }),
  validations: {
    surname: { required },
    name: { required },
    dateOfBirth: { required },
    tel: {
      required,
      minLength: minLength(7),
      maxLength: maxLength(11),
    },
    customerGroup: { required },
    city: { required },
    typeDocument: { required },
    dateOfIssue: { required },
  },
  methods: {
    openMenu(i) {
      setTimeout(() => {
        document.querySelector(`#${i}`).classList.add("active");
      }, 100);
    },
    updateCustomerGroup(el) {
      if (this.customerGroup.find((i) => i === el)) {
        this.customerGroup = this.customerGroup.filter((i) => i !== el);
      } else this.customerGroup.push(el);
    },
    prepared() {
      document.querySelector(".message").classList.add("active");

      setTimeout(() => {
        document.querySelector(".message").classList.remove("active");
      }, 3000);
    },
  },
  mounted() {
    document.onclick = () => {
      if (document.querySelector(".form__menu.active")) {
        document.querySelector(".form__menu.active").classList.remove("active");
      } else return;
    };
  },
};
</script>

<style lang="scss">
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: #fafafa;
}
.container {
  max-width: 1000px;
  margin: 0 auto;
  background-color: #fff;
  border-radius: 5px;
  padding: 1rem;
  box-shadow: 0px 10px 40px rgba(0, 0, 0, 0.3);
}

.card {
  border: 1px solid #ddd;
  border-radius: 5px;
  padding: 1rem;
  margin-top: 1rem;
  background-color: #fefefe;
}

.btn {
  padding: 10px 20px;
  margin-top: 1rem;
  border: none;
  border-radius: 3px;
  font-size: 1.1rem;
  background-color: rgb(38, 0, 255);
  text-transform: uppercase;
  font-weight: 600;
  letter-spacing: 0.0892857143em;
  color: #fff;
  box-shadow: 0 3px 1px -2px rgba(0, 0, 0, 0.3), 0 2px 2px 0 rgba(0, 0, 0, 0.2),
    0 1px 5px 0 rgba(0, 0, 0, 0.2);
  &--disabled {
    background-color: rgba(38, 0, 255, 0.473);
    cursor: not-allowed;
  }
}

.message {
  position: fixed;
  top: 1rem;
  right: 1rem;
  left: -350px;
  max-width: 300px;
  padding: 1rem;
  border: 1px solid #ddd;
  border-radius: 10px;
  background-color: #fff;
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.3);
  display: flex;
  align-items: center;
  transition: 0.5s;
  &.active {
    left: 1rem;
  }
  &__logo {
    width: 30px;
    height: 30px;
    background-color: rgb(0, 212, 0);
    display: flex;
    align-items: center;
    justify-content: center;
    color: #fff;
    border-radius: 50%;
    margin-right: 1rem;
  }
  &__text {
    h3 {
      margin: 0 0 0.5rem 0;
    }
  }
}

.form {
  &__grid {
    display: grid;
    grid-gap: 30px;
    margin-top: 30px;
    &--3 {
      grid-template-columns: repeat(3, 1fr);
      @media (max-width: 600px) {
        grid-template-columns: repeat(1, 1fr);
      }
    }
    &--2 {
      grid-template-columns: repeat(2, 1fr);
      @media (max-width: 600px) {
        grid-template-columns: repeat(1, 1fr);
      }
    }
  }
  &__group {
    font-size: 1.1rem;
    position: relative;
    &--checkbox {
      display: flex;
      align-items: center;
    }
    &--radio {
      display: flex;
      justify-content: space-between;
      flex-direction: column;
      div {
        display: flex;
        align-items: center;
        div + div {
          margin: 10px;
        }
      }
    }
    &--error {
      .form__input {
        box-shadow: 0 3px 1px -1px rgba(252, 0, 0, 0.4),
          0 2px 2px 1px rgba(252, 0, 0, 0.3), 0 1px 5px 0 rgba(252, 0, 0, 0.3);
        &:hover,
        &:focus {
          box-shadow: 0 3px 1px 0px rgba(252, 0, 0, 0.4),
            0 2px 2px 2px rgba(252, 0, 0, 0.3), 0 1px 5px 0 rgba(252, 0, 0, 0.3);
        }
        &::placeholder {
          color: rgba(252, 0, 0, 0.7);
        }
      }
    }
    &--success {
      .form__input {
        box-shadow: 0 3px 1px -1px rgba(0, 170, 0, 0.4),
          0 2px 2px 1px rgba(0, 170, 0, 0.3), 0 1px 5px 0 rgba(0, 170, 0, 0.3);
        &:hover,
        &:focus {
          box-shadow: 0 3px 1px -1px rgba(0, 170, 0, 0.4),
            0 2px 2px 1px rgba(0, 170, 0, 0.3), 0 1px 5px 0 rgba(0, 170, 0, 0.3);
        }
      }
    }
  }
  &__menu {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    transform: scale(0);
    transition: 0.3s;
    background-color: #fff;
    border: 1px solid #ddd;
    border-radius: 5px;
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
    z-index: 100;
    &.active {
      transform: scale(1);
    }
    div {
      padding: 15px 10px;
      border-top: 1px solid #ddd;
      transition: 0.3s;
      display: flex;
      align-items: center;
      &.active {
        background-color: rgba(238, 238, 238, 0.5);
      }
      &:first-child {
        border-top: none;
      }
      &:hover {
        background-color: rgba(238, 238, 238, 0.5);
      }
    }
  }
  &__title {
    margin-top: 0;
  }
  &__input {
    padding: 15px 10px;
    border: none;
    box-shadow: 0 3px 1px -2px rgba(0, 0, 0, 0.2),
      0 2px 2px 0 rgba(0, 0, 0, 0.14), 0 1px 5px 0 rgba(0, 0, 0, 0.12);
    width: 100%;
    transition: 0.2s;
    max-width: 100%;
    font-size: 1.1rem;
    box-sizing: border-box;
    border-radius: 4px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    &-light {
      color: rgb(107, 107, 107);
    }
    &:hover {
      box-shadow: 0 3px 1px -2px rgba(0, 0, 0, 0.3),
        0 2px 2px 0 rgba(0, 0, 0, 0.2), 0 1px 5px 0 rgba(0, 0, 0, 0.2);
    }
    &:focus {
      outline: none;
      box-shadow: 0 3px 1px -2px rgba(38, 0, 252, 0.4),
        0 2px 2px 0 rgba(38, 0, 255, 0.3), 0 1px 5px 0 rgba(38, 0, 255, 0.3);
    }
    &--checkbox {
      width: 20px;
      height: 20px;
      margin-right: 10px;
    }
    &--radio {
      width: 20px;
      height: 20px;
      margin: 0 10px 0 0;
    }
  }
  &__arrow {
    position: absolute;
    top: 15px;
    right: 10px;
    // &::before,
    // &::after {
    //   content: "";
    //   position: absolute;
    //   width: 12px;
    //   height: 2px;
    //   background-color: rgb(116, 116, 116);
    // }
    // &::before {
    //   transform: rotate(45deg);
    //   left: -10px;
    // }
    // &::after {
    //   transform: rotate(-45deg);
    //   right: -10px;
    // }
  }
  &__error-message {
    position: absolute;
    color: rgba(252, 0, 0, 0.7);
    font-size: 0.8rem;
    bottom: -17px;
  }
  &__counter {
    position: absolute;
    right: 10px;
    top: 15px;
    color: rgb(116, 116, 116);
  }
}
</style>
