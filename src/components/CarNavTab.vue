<template>
  <div>
    <div>
      <b-card no-body>
        <b-tabs pills card align="center">
          <template v-for="(items, index) in content">
            <b-tab
              v-if="index < 4"
              :key="index"
              :title="items.tag"
              :active="index == 0"
            >
              <b-card-text>
                <div v-for="(item, key1) in items.series_list.item" :key="key1">
                  <p class="card-text text-center" v-if="key1 < 5" :id="'carnavtab_' + key1.toString()">
                    {{ item.series_name }}, {{ item.price }}
                  </p>
                </div>
              </b-card-text>
            </b-tab>
          </template>
        </b-tabs>
      </b-card>
    </div>
  </div>
</template>

<script>
export default {
  name: "CarNavTab",
  props: {
    content: {
      type: Array,
    },
  },
  data() {
    return {};
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
