<template>
  <div>
    <div class="title">
      <h1>Affix with dynamic relative element</h1>
      <p>Green and red elements should be sticky</p>
    </div>

    <div class="results">
      <div id="el-row">
        <div class="el-col el-col-12">
          <affix class="affix-left" relative-element-selector=".results" :offset="{ top: 0, bottom: 0 }" ref="affixleft" :delayed="true">
            <div class="left-filters">
              <button @click="doRemoveResults">- Remove 10 results</button>
              <button @click="doAddResults">+ Add 10 results</button>
            </div>
          </affix>

          <ul class="left-results">
            <li class="left-results-result" v-for="i in results" :key="i"></li>
          </ul>
        </div>

        <div class="el-col el-col-12">
          <affix class="affix-right" relative-element-selector=".results" :offset="{ top: 0, bottom: 0 }" ref="affixright" :delayed="true">
            <div class="right"></div>
          </affix>
        </div>
      </div>

      <div class="clear"></div>
    </div>
  </div>
</template>

<script>
import Affix from './components/Affix'
// import Affix from 'vue-affix/src/affix'

export default {
  name: 'app',
  data () {
    return {
      results: 0
    }
  },

  components: {
    Affix
  },

  mounted () {
    setTimeout(() => {
      this.results = 30
      this.$refs.affixleft.start()
      this.$refs.affixright.start()
    }, 1000)
  },

  methods: {
    doAddResults () {
      this.results = this.results + 10
      this.$refs.affixleft.update()
      this.$refs.affixright.update()
    },

    doRemoveResults () {
      if (this.results >= 10) this.results = this.results - 10
    }
  }
}
</script>

<style>
.clear {
  clear: both;
}

.title {
  text-align: center;
  padding: 4rem;
}

.left-filters {
  background: green;
  display: block;
  height: 100px;
}

.left-results {
  list-style: none;
  padding: 0 10px 0 0;
}

.left-results-result {
  display: block;
  background: grey;
  height: 50px;
  margin-bottom: 10px;
  border-radius: 3px;
}

.right {
  background: red;
  display: block;
  height: 799px;
}

.results {
  margin-bottom: 200px;
  min-height: 799px;
}

.affix-left.affix,
.affix-left.affix-bottom {
  width: 50%;
}

.affix-right.affix,
.affix-right.affix-bottom {
  width: 50%;
}
</style>
