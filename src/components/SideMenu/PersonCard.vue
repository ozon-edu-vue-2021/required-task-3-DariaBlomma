<template>
  <div class="person">
    <div class="person__photo">
      <img :src="person.picture" alt="photo" />
    </div>
    <div class="person__info">
      <div class="person__info-name">
        <b>{{ person.name }} ({{ person.age }})</b>
      </div>

      <div class="person__info-email">
        <span class="person__info-title-line">
          <EmailSvg class="email-svg" />
          <b>Почта: </b>
        </span>
        {{ person.email }}
      </div>
      <div class="person__info-email">
        <span class="person__info-title-line">
          <DateSvg class="date-svg" />
          <b>Дата регистрации:</b>
        </span>
        {{ formatedDate }}
      </div>
      <div class="person__info-about">
        <span class="person__info-title-line">
          <AboutSvg class="about-svg" />
          <b>О себе:</b>
        </span>
        {{ person.about }}
      </div>
    </div>
  </div>
</template>

<script>
import { format } from "date-fns";
import EmailSvg from "@/assets/images/email.svg";
import DateSvg from "@/assets/images/date.svg";
import AboutSvg from "@/assets/images/about.svg";

export default {
  props: {
    person: {
      type: Object,
      default: null,
    },
  },
  components: {
    EmailSvg,
    DateSvg,
    AboutSvg,
  },
  computed: {
    formatedDate() {
      return format(new Date(this.person.registered), "MM.dd.yyyy hh:mm:ss");
    },
  },
};
</script>

<style scoped>
.person {
  display: grid;
  grid-template-columns: 50px 1fr;
  grid-gap: 8px;
}

.person__photo img {
  height: 50px;
  width: 50px;
  border-radius: 50%;
}

.person__info {
  display: grid;
  grid-gap: 8px;
}

.person__info-title-line {
  display: flex;
  align-items: center;
  margin-bottom: 5px;
}

.person__info-name {
  margin-bottom: 10px;
}

.person__info-email,
.person__info-about {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  /* align-items: center; */
}

.email-svg,
.date-svg,
.about-svg {
  margin-right: 10px;
}

.date-svg {
  align-self: center;
}
</style>
