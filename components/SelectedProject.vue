<script setup>
import { emitLeaveHovered, emitHovered } from "~/utils/emit";

const props = defineProps({
  data: {
    type: Object,
    required: true,
  },
  showBanner: {
    type: Boolean,
    required: false,
    default: true,
  },
});
</script>

<template>
  <div class="c-projects">
    <infinite content="Here are my selected project" v-if="showBanner" />
    <infinite
      v-if="showBanner"
      content="Here are my selected project"
      variant="reverse"
      color="green"
    />

    <NuxtLink
      @mouseleave="emitLeaveHovered"
      @mouseover="emitHovered"
      class="c-projects__item"
      v-for="(item, index) in data"
      :key="index"
      :to="`/portfolio/${item.project.uid}`"
    >
      <div class="c-projects__content">
        <img class="c-projects__img" :src="item.project_img.url" alt="" />
        <div class="c-projects__texts">
          <h3 class="c-projects__titles">{{ item.project_title[0].text }}</h3>
          <p class="c-projects__tags">
            <span
              v-for="({ text }, i) in item.project_stack"
              :class="text"
              :key="i"
              >{{ text }}</span
            >
          </p>
        </div>
      </div>
    </NuxtLink>
  </div>
</template>

<style lang="scss">
.c-projects {
  padding-top: rem(100);
  &__content {
    width: 100%;
    max-height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
  }
  &__img {
    order: 2;
    @include medium-up {
      max-width: rem(450);
    }
    max-height: 50%;
  }
  &__texts {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    width: 50%;
  }
  &__titles {
    font-size: 7vw;
    @include medium-up{
        font-size: 4vw;
      }
    font-weight: 600;
    text-transform: uppercase;
    margin: 0;
    text-align: center;
  }

  &__tags {
    display: flex;
    gap: rem(5);
    span {
      display: block;
      border: 1px solid $black;
      border-radius: rem(5);
      padding: rem(5) rem(10);
    }
  }
  &__item {
    &:nth-child(n) {
      margin-top: rem(50);
    }
    align-items: center;
    display: flex;
    border: 2px solid black;
    color: $black;
    text-decoration: none;
    padding: rem(20);
    margin: rem(20);
  }
  .VueJs, .NuxtJs {
    background-color: #3cffa7;
  }
  .Firebase {
    background-color: #ffcb2b;
  }
  .UE5 {
    background-color: #ff5f5f;
  }
  .OpenAi{
    background-color: #9b59b6;
  }
  .Supabase{
    background-color: #1abc9c;
  }
  .ReactJs{
    background-color: #00d8ff;
  }
  .AstroJs{
     background-color:hsl(224, 100%, 85%);
  }
  .GSAP{
   background-color:#0ae448;
  }
}
</style>
