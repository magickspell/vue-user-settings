<template>
  <div class="sip-calls">
    <div class="sip-calls-switcher"
         @click="handleSwitch"
    >
      <span>Звонок через SIP</span>
      <div class="sip">
        <div class="sip-inner"></div>
      </div>
    </div>
    <p>
      Включите эту функцию чтобы Авито и другие площадки не блокировали ваш аккаунт.
      Будет выглядеть так, будто звонки совершаются с разных номеров.
    </p>
  </div>
</template>

<script>
export default {
  name: 'SipTogler',
  methods: {
    handleSwitch() {
      const el = document.getElementsByClassName('sip-calls-switcher')[0]
      if (el.classList.contains('active')) el.classList.remove('active')
      else el.classList.add('active')
    },
  }
}
</script>

<style lang="scss">
.sip-calls-switcher {
  display: flex;
  align-items: center;
  cursor: pointer;

  .sip {
    margin-left: 4px;
    display: inline-flex;
    justify-content: flex-start;
    border: 3px solid lightgray;
    border-radius: 20px;
    width: 48px;
    height: 32px;
    background: white;
    color: white;
    transition: 0.3s;

    .sip-inner {
      background: lightgray;
      width: 24px;
      height: 26px;
      border-radius: 20px;
      transition: 0.3s;
    }
  }

  &.active {
    .sip {
      border: 3px solid #2dc574;
      justify-content: flex-end;

      .sip-inner {
        background: #2dc574;
      }
    }
  }
}
</style>