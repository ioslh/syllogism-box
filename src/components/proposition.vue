<template>
  <div class="proposition">
    <span class="quantifier">{{ quantifierText }}</span>
    <span class="term subject" :style="styles[subjectRole]">{{ propsition.subject }}</span>
    <span class="copula">{{ qualityText }}</span>
    <span class="term predicate" :style="styles[predicateRole]">{{ propsition.predicate }}</span>
  </div>
</template>

<script lang="ts" setup>
import { quantity, quality, Proposition, Quantifier, Quality, TERM_ROLE } from '@/shared/syllogism'
import { i18n } from '@/shared/translate'

const { propsition } = defineProps<{
  propsition: Proposition
  subjectRole: TERM_ROLE
  predicateRole: TERM_ROLE
}>()


const quantifierText = $computed(() => {
  if (quantity[propsition.mood] === Quantifier.PARTICULAR) return i18n.value.some
  return quality[propsition.mood] === Quality.AFFITMATIVE ? i18n.value.all : i18n.value.no
})

const qualityText = $computed(() => {
  if (quantity[propsition.mood] === Quantifier.UNIVERSAL) {
    return quality[propsition.mood] === Quality.AFFITMATIVE ? i18n.value.allis : i18n.value.is
  }
  return quality[propsition.mood] === Quality.AFFITMATIVE ? i18n.value.is : i18n.value.isnot
})

const majorStyle = {
  color: 'rgb(182 36 86 / 58%)',
  background: '#fde0e0'
}

const minorStyle = {
  color: 'rgb(244 152 110)',
  background: '#cccccc85',
}

const middleStyle = {
  color: '#6b60bb',
  background: 'rgb(221 206 217)'
}

const styles = {
  [TERM_ROLE.MAJOR]: majorStyle,
  [TERM_ROLE.MINOR]: minorStyle,
  [TERM_ROLE.MIDDLE]: middleStyle,
}

</script>

<style lang="scss" scoped>
.proposition {
  font-size: 36px;
  font-weight: 900;
  color: #888;
}

.term {
  border-radius: 4px;
  padding: 0 4px;
}

.quantifier {
  // color: #581;
  margin-right: 4px;
}

.copula {
  // color: #888;
  margin: 0 4px;
}
</style>