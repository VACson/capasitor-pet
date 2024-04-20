<template>
  <button
    class="base-button"
    :class="getPropsClass()"
    @click="emit('click')"
  >
    <IonSpinner
      v-if="props.loading"
      name="circular"
    />
    <slot />
  </button>
</template>

<script setup lang="ts">
import { IonSpinner } from "@ionic/vue"

type Props = {
  disabled?: boolean
  className?: "disabled" | "danger" | "dark" | "default" | "light" | "outline"
  loading?: boolean
}

const props = withDefaults(defineProps<Props>(), {
  disabled: false,
  className: "default",
  loading: false
})

const emit = defineEmits(["click"])

const classes = {
  disabled: "base-button--disabled",
  danger: "base-button--danger",
  dark: "base-button--dark",
  light: "base-button--light",
  outline: "base-button--outline",
  default: "base-button--default"
}

const getPropsClass = () => {
  if (props.className === "default") return ""
  return classes[props.className]
}
</script>

<style scoped lang="scss">
.base-button {
  width: 100%;
  height: 50px;
  box-sizing: border-box;

  display: flex;
  justify-content: center;
  align-items: center;

  background: transparent;
  background-color: transparent;
  outline: none;
  border: 2px solid var(--ion-color-dark);

  border-radius: 5px;
  padding: 4px 16px;
  line-height: 16px;

  color: var(--ion-color-dark);
  font-size: 16px;
  font-weight: medium;
  text-transform: uppercase;

  transition: 1s;

  & * {
    color: inherit;
    font-size: inherit;
    height: 16px;
  }

  &--dark {
    background-color: var(--ion-color-dark);
    color: var(--ion-color-light);
    border: 2px solid var(--ion-color-dark);
  }

  &--light {
    background-color: var(--ion-color-light);
    color: var(--ion-color-dark);
    border: 2px solid var(--ion-color-light);
  }

  &--outline {
    background-color: var(--ion-color-dark);
    color: var(--ion-color-light);
    border: 2px solid var(--ion-color-light);
  }
}
</style>