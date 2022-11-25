<template>
  <div class="other-settings">
          <span>
            Прочие настройки
          </span>
    <div>
      <div class="other-settings-body">
        <div class="other-settings-body-hours">
          <label for="hours">Часовой пояс</label>
          <select name="hours" id="">
            <option value="moscow">Москва</option>
            <option value="samara">Самара</option>
            <option value="kaliningrad">Калининград</option>
          </select>
        </div>
        <div class="other-settings-body-checkbox">
          <label for="checkbox"></label>
          <input type="checkbox" name="checkbox">
          <label>Автоматически переходить к новым объявлениям</label>
          <i class="tooltip">
            i
            <span class="tooltiptext">
              Lorem ipsum dolor.
            </span>
          </i>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'OtherSettings',
}
</script>

<style lang="scss">
/* tooltip */
i {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  color: lightgray;
  font-style: normal;
  width: 24px;
  min-width: 24px;
  height: 24px;
  min-height: 24px;
  border: 1px solid lightgray;
  border-radius: 100%;
  cursor: help;

  &.tooltip .tooltiptext {
    width: 120px;
    background-color: #26A763;
    color: #fff;
    text-align: center;
    border-radius: 8px;
    padding: 4px;
    position: absolute;
    z-index: 1;
    top: 100%;
    left: 50%;
    margin-left: -60px;
    margin-top: 8px;
    font-size: 14px !important;
    opacity: 0;
    transition: 0.3s;
    font-weight: 400;
  }

  &.tooltip:hover .tooltiptext {
    opacity: 1;
  }
}
</style>