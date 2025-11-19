<script>
import Title from './sections/Title.vue'
import Abstract from './sections/Abstract.vue'
import BibTeX from './sections/BibTeX.vue'
import Carousel from './sections/Carousel.vue'
import Overview from './sections/Overview.vue'
import Bench from './sections/Bench.vue'
import MazeVariations from './sections/MazeVariations.vue'
import Table from './sections/Table.vue'
import PerformanceComparison from './sections/PerformanceComparison.vue'
import CaseDemonstration from './sections/CaseDemonstration.vue'

export default {
  components: {
    Title,
    Abstract,
    BibTeX,
    Carousel,
    Overview,
    Bench,
    MazeVariations,
    PerformanceComparison,
    CaseDemonstration
  }
}
</script>

<template>
  <Title/>
  <Carousel/>
  <Overview/>
  <Abstract/>
  <MazeVariations/>
  <Table/>
  <Bench/>
  <PerformanceComparison/>
  <CaseDemonstration/>
  <BibTeX/>
</template>
