<template>
  <div class="content">
    <StudentCard
      v-for="student in students"
      :key="student.id"
      :student="student"
      @save="updateStudentRecord(student, $event)"
    />
  </div>
</template>

<script>
import StudentCard from "@/components/StudentCard";

export default {
  name: "HomeView",
  components: {
    StudentCard,
  },
  data() {
    return {
      students: [
        {
          id: 1,
          name: "Кумакин Филипп Сергеевич",
          passport: "666666666",
        },
        {
          id: 2,
          name: "Иванов Иван Иванович",
          passport: "6666",
        },
      ],
    };
  },
  methods: {
    updateStudentRecord(record, data) {
      console.log("test", data);
      record.name = data.name;
      record.passport = data.passport;
    },
  },
};
</script>

<style lang="scss" scoped>
@import "@/assets/styles/common.scss";

.content {
  @include setProperty(margin-top, 14px, 16px, 24px, 32px);
  box-shadow: 0 0 4px 0 rgba(0, 0, 0, 0.3);

  @include sm {
    box-shadow: 0 0 6px 0 rgba(0, 0, 0, 0.3);
  }
}
</style>
