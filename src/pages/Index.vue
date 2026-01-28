<template>
  <div>
    <Header ref="headerRef" />
    <SectionOne />
    <SectionTwo />
    <SectionThree />
  </div>
</template>

<script>
import Header from "@/components/Header.vue"
import SectionOne from "@/components/SectionOne.vue"
import SectionTwo from "@/components/SectionTwo.vue"
import SectionThree from "@/components/SectionThree.vue"

export default {
  components: {
    Header,
    SectionOne,
    SectionTwo,
    SectionThree
  }
}
</script>
