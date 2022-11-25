<template>
  <div class="user-info-body-item">
    <label :for="name">{{ label }}</label>
    <input
        :value="value"
        :name="name"
        type="text"
        placeholder="..."
    >
  </div>
</template>

<script>
export default {
  name: 'InputItem',
  props: {
    name: String,
    value: String,
    label: String,
  },
}
</script>

<style lang="scss">
input[type="checkbox"],
input[type="radio"] {
  position: relative;
  width: 18px;
  height: 0;
  margin: 0 8px;
  transition: 0s;

  &:before {
    display: flex;
    justify-content: center;
    align-items: center;
    content: '';
    border: 1px solid #2dc574;
    position: absolute;
    width: 18px;
    height: 18px;
    z-index: 10;
    color: white;
  }

  &:checked {
    &:before {
      content: '✓';
      background: #2dc574;
    }
  }
}

input[type="radio"] {
  bottom: 12px;

  &:before {
    border-radius: 100%;
  }

  &:checked {
    &:after {
      position: absolute;
      left: 3px;
      top: 3px;
      width: 14px;
      height: 14px;
      background: #2dc574;
      content: '';
      border-radius: 100%;
      z-index: 20;
    }

    &:before {
      content: '';
      background: white;
    }
  }
}

input {
  height: 32px;
  width: 240px;
  padding: 8px;
  border: 1px solid lightgray;
  border-radius: 4px;
  color: gray;
  outline: none;
  transition: 0.3s;

  &:focus {
    border: 1px solid #2dc574;
  }
}
</style>