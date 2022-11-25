<template>
  <h3 v-if="loading">Loading...</h3>
  <div class="settings-wrapper" v-else-if="!loading">
    <h1>Настройки</h1>
    <section>
      <form @submit.prevent>
        <div class="save-button">
          <div></div>
          <button @click="saveData">Сохранить</button>
        </div>
        <OtherSettings/>
        <div class="new-notification">
          <span>Оповещения о новых подборках</span>
          <div class="new-notification-items">
            <p>
              Выберите, куда будут приходить уведомления при появлении автомобилей,
              которые подходят под критерии вашей подборки.
            </p>
            <p class="p-title">Уведомления</p>
            <div class="new-notification-items-off">
              <input name="notification" value="notification-off" type="radio" :checked="(this.notifyOff)">
              <label for="notification-off">Выкл</label>
            </div>
            <hr>
            <div class="new-notification-items-email">
              <input name="notification" value="notification-email" type="radio" :checked="(!this.notifyOff)">
              <label for="notification-email">Email</label>
              <input v-if="email" type="text" :value="emailString" @input="event => emailString = event.target.value">
              <b v-if="!email" @click="email = !email">&#9997;</b>
              <b v-if="email" @click="email = !email">&#10060;</b>
            </div>
            <hr>
            <div class="new-notification-items-telegram">
              <input name="notification" value="notification-telegram" type="radio">
              <label for="notification-telegram">Telegram ID</label>
              <input v-if="telegram" type="text">
              <b v-if="!telegram" @click="telegram = !telegram">&#9997;</b>
              <b v-if="telegram" @click="telegram = !telegram">&#10060;</b>
            </div>
          </div>
        </div>
        <div class="user-info">
          <span>Учётная запись</span>
          <div class="user-info-body">
            <div class="user-info-body">
              <InputItem :value="companyName" label="Компания" name="companyName"></InputItem>
              <InputItem :value="login" label="Логни" name="login"></InputItem>
              <InputItem :value="phone" label="Номер телефона" name="phone"></InputItem>
              <InputItem :value="fName" label="Имя" name="fName"></InputItem>
              <InputItem :value="lName" label="Фамилия" name="lName"></InputItem>
            </div>
          </div>
        </div>
        <SipTogler/>
      </form>
    </section>
  </div>
</template>

<script>
import InputItem from "@/component/Input-Item";
import SipTogler from "@/component/SipTogler";
import OtherSettings from "@/component/OtherSettings";

require('normalize.css')

export default {
  name: 'settingsScreen',
  components: {SipTogler, InputItem, OtherSettings},
  props: {
    msg: String
  },
  data() {
    return {
      loading: true,
      telegram: false,
      email: false,
      emailString: '',
      notifyOff: true,
      uid: '1904226',
      companyName: '',
      fName: '',
      lName: '',
      login: '',
      phone: '',
      allData: {}
    }
  },
  methods: {
    async fetchData() {
      await fetch(`https://av100.pro/api/user/${this.uid}`, {
        method: 'GET',
        mode: 'cors',
        headers: {
          'Content-Type': 'application/json',
          'X-Api-Key': '8bcfb6e1-4fa8-4fae-872c-a435bbdbe8d9',
          'X-User-Token': 'bdd40716-212d-484a-9e73-a0a1d599252c'
        }
      }).then((res) => {
        return res.json()
      }).then((data) => {
        this.fName = data.fname
        this.lName = data.lname
        this.login = data.login
        this.phone = data.phone
        this.companyName = data.companyname
        this.emailString = data.email
        this.notifyOff = (data.notifytypestring === '')
        this.email = (data.notifytypestring === 'Email')
        this.allData = data
        this.loading = false
      }).catch((e) => {
        console.warn(e)
        alert(e)
      })
    },
    async saveData() {
      await fetch(`https://av100.pro/api/user/${this.uid}`, {
        method: 'PUT',
        mode: 'cors',
        headers: {
          'Content-Type': 'application/json',
          'X-Api-Key': '8bcfb6e1-4fa8-4fae-872c-a435bbdbe8d9',
          'X-User-Token': 'bdd40716-212d-484a-9e73-a0a1d599252c'
        },
        body: JSON.stringify({
          ...this.allData,
          email: this.emailString,
        })
      })
          .catch((e) => {
            console.warn(e)
            alert(e)
          })
    },
  },
  mounted() { // lifecycle when component mounted
    this.fetchData();
  }
}
</script>

<style lang="scss">
.settings-wrapper {
  overflow-x: hidden;

  h1 {
    background: lightgray;
    font-size: 32px;
    padding: 8px 20px;
  }

  section {
    max-width: 720px;

    form {
      .save-button {
        button {
          width: auto;
          height: 40px;
          font-weight: 600;
          font-size: 14px;
          color: #fff;
          background: #2dc574;
          border: none;
          outline: none;
          cursor: pointer;
          transition: 0.3s;

          &:hover {
            background: #26A763;
          }
        }
      }

      .save-button, .other-settings, .new-notification, .user-info, .sip-calls {
        display: grid;
        grid-template-columns: 250px 490px;
        margin: 24px 0;

        span {
          font-size: 20px;
          font-weight: 600;
        }

        p {
          color: gray;
        }

        .p-title {
          font-size: 18px;
          font-weight: 600;
          color: black;
          margin: 16px 0 12px;
        }

        select {
          height: 28px;
          width: 216px;
          margin-left: 24px;
          font-size: 16px;

          option {
            background: #26A763;
            color: white;
          }
        }

        hr {
          margin: 16px 0;
        }

        .other-settings-body-checkbox {
          margin-top: 12px;
          display: flex;
          gap: 8px;

          label {
            max-width: 60%;
            font-size: 14px;
          }
        }
      }

      .other-settings {
        .other-settings-body-hours {
          padding-top: 20px;
          border-top: 1px solid gray;
        }
      }

      .user-info {
        .user-info-body-item {
          display: flex;
          justify-content: space-between;
          margin: 12px 0 0;
        }
      }

      .new-notification {
        .new-notification-items {
          .new-notification-items-telegram, .new-notification-items-email, .new-notification-items-off {
            display: flex;
            gap: 20px;
            align-items: center;

            label {
              line-height: 32px;
            }
          }
        }
      }
    }
  }
}

@media (max-width: 800px) {
  .settings-wrapper {
    min-width: 320px;

    h1 {
      font-size: 26px;
    }

    section {
      margin: 0 8px 0 0;

      form {
        .new-notification {
          .new-notification-items {
            .new-notification-items-telegram, .new-notification-items-email, .new-notification-items-off {
              gap: 8px;
            }
          }
        }

        .save-button, .other-settings, .new-notification, .user-info, .sip-calls {
          grid-template-columns: 320px;

          input {
            width: 220px;
          }

          select {
            width: 180px;
          }
        }
      }
    }
  }
}
</style>