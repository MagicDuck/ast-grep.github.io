<script setup lang="ts">
import IconDown from './utils/IconDown.vue'
import Error from './utils/Error.vue'

const props = defineProps({
  error: String,
})
const strictness = defineModel('strictness')
const selector = defineModel('selector')

function selectAll(e: FocusEvent) {
  const input = e.target as HTMLInputElement
  input.select()
}
</script>

<template>
  <div class="pattern-config">
    <label>
      <a target="_blank" href="https://ast-grep.github.io/advanced/match-algorithm.html">ⓘ</a>
      Strictness:
      <select class="strictness-select" v-model="strictness">
        <option value="smart">Smart</option>
        <option value="ast">Ast</option>
        <option value="cst">Cst</option>
        <option value="relaxed">Relaxed</option>
        <option value="signature">Signature</option>
      </select>
      <IconDown/>
    </label>
    <label>
      <a target="_blank" href="https://ast-grep.github.io/advanced/faq.html#my-pattern-does-not-work-why">ⓘ</a>
      Selector:
      <input @focus="selectAll" class="selector-input" type="text" v-model="selector"/>
    </label>
    <Error class="error" :error="error"/>
  </div>
</template>

<style scoped>
.pattern-config {
  z-index: 2;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  border-top: 1px solid var(--vp-c-bg-soft);
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
  font-size: 12px;
  border-radius: 10px 10px 0 0;
  padding: 0.5em 1em;
}
.strictness-select {
  cursor: pointer;
  padding-left: 0.25em;
}
.selector-input {
  background: var(--vp-c-bg-alt);
  border-radius: 5px;
  height: 25px;
  padding: 8px;
}
.error {
  width: 100%;
  margin: 0.5em 0 0.25em;
}
</style>