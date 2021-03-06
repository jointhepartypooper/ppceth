<template>
  <button
    class="m-button"
    @click="handleClick"
    :disabled="disabled"
    :class="[
      type && 'm-button-' + type,
      size && 'm-button-' + size,
      {
        'm-button-type-plain': plain,
        'm-button-rounded': round,
        'm-button-block': block,
        active: active,
        clicked: effect && clicked && !active,
      },
    ]"
  >
    <slot></slot>
  </button>
</template>
<script type="text/javascript">
// Returns a function, that, as long as it continues to be invoked, will not
// be triggered. The function will be called after it stops being called for
// N milliseconds. If `immediate` is passed, trigger the function on the
// leading edge, instead of the trailing.
function debounce(func, wait, immediate) {
  var timeout;
  return function () {
    var context = this,
      args = arguments;
    var later = function () {
      timeout = null;
      if (!immediate) func.apply(context, args);
    };
    var callNow = immediate && !timeout;
    clearTimeout(timeout);
    timeout = setTimeout(later, wait);
    if (callNow) func.apply(context, args);
  };
}

export default {
  name: "m-button",
  props: {
    type: {
      type: String,
      default: "",
    },
    effect: {
      type: Boolean,
      default: true,
    },
    size: {
      type: String,
      default: "",
    },
    disabled: {
      type: Boolean,
      default: false,
    },
    active: {
      type: Boolean,
      default: false,
    },
    plain: {
      type: Boolean,
      default: false,
    },
    round: {
      type: Boolean,
      default: false,
    },
    block: {
      type: Boolean,
      default: false,
    },
    router: [String, Object],
  },
  data() {
    return {
      clicked: false,
      dbclick: null,
    };
  },
  methods: {
    handleClick(e) {
      if (this.router && this.$router) {
        if (typeof this.router === "string") {
          this.$router.push({ path: this.router });
          return false;
        } else if (typeof this.router === "object") {
          this.$router.push(this.router);
          return false;
        }
      }

      if (!this.dbclick)
        this.dbclick = debounce(function () {
          this.clicked = true;
          this.$emit("mbclick", e);
          setTimeout(() => {
            this.clicked = false;
          }, 500);
        }, 200);

      this.dbclick();
    },
  },
};
</script>

<style lang="scss">
a.m-button {
  text-decoration: none;
  color: inherit;
}
.m-button {
  color: #fff;
  background-image: none;
  background-color: #727b84;
  display: inline-block;
  padding: 7px 21px;
  font-size: 14px;
  font: inherit;
  font-weight: 400;
  line-height: 1.42857143;
  text-align: center;
  vertical-align: middle;
  white-space: nowrap;
  touch-action: manipulation;
  cursor: pointer;
  outline: none;
  border-radius: 4px;
  border: solid 1px #727b84;
  transition: color 0.15s ease-in-out, background-color 0.15s ease-in-out,
    border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
  user-select: none;

  -moz-user-select: none;
  -o-user-select: none;
  -khtml-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
}
.m-button:hover {
  background-color: #868e96;
  border: solid 1px #868e96;
}
.m-button:active,
.m-button.active {
  opacity: 0.9;
  position: relative;
}
.m-button.active:after {
  content: "";
  position: absolute;
  display: block;
  top: -4px;
  left: -4px;
  bottom: -4px;
  right: -4px;
  opacity: 0.35;
  border: solid 6px;
  border-radius: 6px;
  border-color: inherit;
}
.m-button + .m-button {
  margin-left: 10px;
}
.m-button:disabled,
.m-button.disabled {
  cursor: not-allowed;
  color: rgba(0, 0, 0, 0.25);
  background-color: #f5f5f5;
  border-color: #d9d9d9;
}
.m-button.m-button-rounded {
  border-radius: 50px;
}
.m-button.m-button-max {
  padding: 15px 45px;
  font-size: 16px;
}
.m-button.m-button-large {
  padding: 10px 30px;
}
.m-button.m-button-small {
  padding: 5px 15px;
  font-size: 13px;
}
.m-button.m-button-mini {
  padding: 4px 12px;
  font-size: 12px;
}
.m-button.m-button-block {
  display: block;
  width: 100%;
}
.m-button.m-button-block + .m-button.m-button-block {
  margin-left: auto;
  margin-top: 10px;
}
.m-button.m-button-info {
  color: #fff;
  background-color: #2db7f5;
  border-color: #2db7f5;
}
.m-button.m-button-info:hover {
  background-color: #36c1fa;
  border-color: #36c1fa;
}
.m-button.m-button-info:disabled,
.m-button.m-button-info.disabled {
  cursor: not-allowed;
  background-color: #6bccea;
  border-color: #6bccea;
}
.m-button.m-button-primary {
  color: #fff;
  background-color: #7952b3;
  border-color: #7952b3;
}
.m-button.m-button-primary:hover {
  background-color: #8e74b4;
  border-color: #8e74b4;
}
.m-button.m-button-primary:disabled,
.m-button.m-button-primary.disabled {
  cursor: not-allowed;
  background-color: #9e98ce;
  border-color: #9e98ce;
}
.m-button.m-button-success {
  color: #fff;
  background-color: #03b976;
  border-color: #03b976;
}
.m-button.m-button-success:hover {
  background-color: #05a56a;
  border-color: #05a56a;
}
.m-button.m-button-success:disabled,
.m-button.m-button-success.disabled {
  cursor: not-allowed;
  background-color: #56ceb0;
  border-color: #56ceb0;
}
.m-button.m-button-danger {
  color: #fff;
  background-color: #f56c6c;
  border-color: #f56c6c;
}
.m-button.m-button-danger:hover {
  background-color: #f78989;
  border-color: #f78989;
}
.m-button.m-button-danger:disabled,
.m-button.m-button-danger.disabled {
  cursor: not-allowed;
  background-color: #fab6b6;
  border-color: #fab6b6;
}
.m-button.m-button-warning {
  color: #fff;
  background-color: #f9aa40;
  border-color: #f9aa40;
}
.m-button.m-button-warning:hover {
  background-color: #fab458;
  border-color: #fab458;
}
.m-button.m-button-warning:disabled,
.m-button.m-button-warning.disabled {
  cursor: not-allowed;
  background-color: #ffc576;
  border-color: #ffc576;
}
.m-button.clicked {
  position: relative;
}
.m-button.clicked:before {
  content: "";
  position: absolute;
  display: block;
  top: -1px;
  left: -1px;
  bottom: -1px;
  right: -1px;
  opacity: 0.8;
  border: solid 0px;
  border-color: inherit;
  border-radius: inherit;
  animation: btn-clicked-effect 0.5s;
}
.m-button.m-button-type-plain {
  color: #868e96;
  border-color: #727b84;
  background-color: transparent;
}
.m-button.m-button-type-plain:hover {
  background-color: #727b84;
  color: #fff;
}
.m-button.m-button-type-plain.m-button-info {
  color: #2db7f5;
  border-color: #36c1fa;
}
.m-button.m-button-type-plain.m-button-info:hover {
  border-color: #2db7f5;
  background-color: #2db7f5;
  color: #fff;
}
.m-button.m-button-type-plain.m-button-primary {
  color: #7952b3;
  border-color: #8e74b4;
}
.m-button.m-button-type-plain.m-button-primary:hover {
  border-color: #7952b3;
  background-color: #7952b3;
  color: #fff;
}
.m-button.m-button-type-plain.m-button-success {
  color: #03b976;
  border-color: #05a56a;
}
.m-button.m-button-type-plain.m-button-success:hover {
  border-color: #03b976;
  background-color: #03b976;
  color: #fff;
}
.m-button.m-button-type-plain.m-button-danger {
  color: #f56c6c;
  border-color: #f78989;
}
.m-button.m-button-type-plain.m-button-danger:hover {
  border-color: #f56c6c;
  background-color: #f56c6c;
  color: #fff;
}
.m-button.m-button-type-plain.m-button-warning {
  color: #f9aa40;
  border-color: #fab458;
}
.m-button.m-button-type-plain.m-button-warning:hover {
  border-color: #f9aa40;
  background-color: #f9aa40;
  color: #fff;
}
.m-button-block + .m-button-block {
  margin-top: 5px;
}
.m-button-group {
  position: relative;
  display: inline-block;
  vertical-align: middle;
}
.m-button-group .m-button {
  position: relative;
  float: left;
  border-radius: 0;
  margin-left: -1px;
}
.m-button-group .m-button:first-child {
  margin-left: 0;
  border-top-left-radius: 4px;
  border-bottom-left-radius: 4px;
}
.m-button-group .m-button:last-child {
  border-top-right-radius: 4px;
  border-bottom-right-radius: 4px;
}
</style>
