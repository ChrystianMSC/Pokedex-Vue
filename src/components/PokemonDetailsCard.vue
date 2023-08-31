<template>
  <v-card
    elevation="5"
    class="rounded-xl mx-auto my-12"
    :max-width="small ? '200' : '354'"
  >
    <v-img
      height="250"
      :src="pokemon.sprites.front_default"
      :class="pokemon.types[0].type.name"
    ></v-img>

    <v-card-title
      class="mt-2 title montserrat-alternates d-flex justify-start align-center"
      >{{ pokemon.name }}
      <div
        v-for="(pokeType, index) in pokemon.types"
        :key="index"
        class="d-flex justify-start gap-10 ml-2"
      >
        <v-img
          :src="getIcon(pokeType.type.name)"
          height="20"
          width="20"
        ></v-img>
      </div>
    </v-card-title>

    <v-card-text>
      <div class="text-subtitle-1 d-flex justify-space-between">
        <span class="title"> Weight</span>
        <span> {{ pokemon.weight / 10 }} kg</span>
      </div>
      <div class="text-subtitle-1 d-flex justify-space-between">
        <span class="title"> Height</span>
        <span> {{ pokemon.height / 10 }} m</span>
      </div>
    </v-card-text>

    <v-divider class="mx-4"></v-divider>

    <v-card-text>
      <p class="text-subtitle-1 title montserrat-alternates">Abilities</p>
      <div
        v-for="ability in pokemon.abilities"
        :key="ability.name"
        class="text-subtitle-1 d-flex justify-space-between"
      >
        <span class="title">
          {{ ability.ability.name.replaceAll("-", " ") }}</span
        >
      </div>
    </v-card-text>
    <v-divider class="mx-4"></v-divider>
    <v-card-text>
      <div class="text-subtitle-1 d-flex flex-column">
        <span class="title text-subtitle-1 montserrat-alternates"> Stats</span>
        <div
          class="stat-wrapper mb-2"
          :key="index"
          v-for="(stat, index) in pokemon.stats"
        >
          <div class="text-subtitle-1 d-flex justify-space-between mb-1">
            <span class="title" style="font-size: 14px">
              {{ stat.stat.name }}
            </span>
            <span class="title" style="font-size: 14px">
              {{ stat.base_stat }}
            </span>
          </div>
          <v-progress-linear
            class="mb-3"
            :model-value="(stat.base_stat / 230) * 100"
            :bg-color="`var(--${pokemon.types[0].type.name}-color)`"
            :color="`var(--${pokemon.types[0].type.name}-color)`"
          ></v-progress-linear>
        </div>
      </div>
    </v-card-text>
  </v-card>
</template>

<script>

export default {
  props: {
    pokemon: {
      type: Object,
      required: true,
    },
    small: {
      type: Boolean,
    },
  },
  methods: {
    getIcon(icon) {
      return require(`@/assets/icons/${icon}.svg`);
    },
  },
};
</script>

<style lang="scss" scoped></style>
