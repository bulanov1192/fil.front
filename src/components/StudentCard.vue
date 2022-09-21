<template>
  <div class="student" :class="loading && 'student--loading'">
    <div class="student__data">
      <div class="student__name">
        <template v-if="editMode">
          <input type="text" placeholder="Введите ФИО" v-model="name" />
        </template>
        <template v-else>
          {{ student.name }}
        </template>
      </div>
      <div class="student__passport">
        <template v-if="editMode">
          <input
            type="text"
            placeholder="Введите номер паспорта"
            v-model="passport"
          />
        </template>
        <template v-else>
          {{ student.passport }}
        </template>
      </div>
    </div>
    <div
      class="student__edit"
      @click="editMode ? saveEdit() : enableEditMode()"
      :class="editMode && 'student__edit--save'"
    >
      <a rel="noopener"></a>
    </div>
    <div
      class="student__delete"
      @click="editMode ? cancelEdit() : deleteStudent()"
      :class="editMode && 'student__edit--cancel'"
    >
      <a rel="noopener"></a>
    </div>
  </div>
</template>

<script>
export default {
  name: "StudentCard",
  props: {
    student: {
      required: true,
      type: Object,
      validator(value) {
        if (!value || typeof value !== "object") {
          return false;
        } else if (
          (!value.id && value.id !== 0) ||
          typeof value.id !== "number"
        ) {
          return false;
        } else if (!value.name || typeof value.name !== "string") {
          return false;
        } else if (!value.passport || typeof value.passport !== "string") {
          return false;
        }
        return true;
      },
    },
  },
  data() {
    return {
      name: "",
      passport: "",
      editMode: false,
      loading: false,
    };
  },
  mounted() {
    this.setInitialData();
  },
  methods: {
    setInitialData() {
      this.name = this.student.name;
      this.passport = this.student.passport;
    },
    enableEditMode() {
      this.editMode = true;
    },
    validateInputs() {
      if (!this.name || !this.passport) {
        return false;
      } else if (!this.name.trim() || !this.passport.trim()) {
        return false;
      }
      return true;
    },
    async saveEdit() {
      if (!this.validateInputs()) {
        return false;
      }
      this.loading = true;
      if (
        this.name !== this.student.name ||
        this.passport !== this.student.passport
      ) {
        await setTimeout(() => {
          this.$emit("save", {
            name: this.name,
            passport: this.passport,
          });
          this.editMode = false;
          this.loading = false;
        }, 1000);
      } else {
        this.editMode = false;
        this.loading = false;
      }
    },
    cancelEdit() {
      this.editMode = false;
      this.setInitialData();
    },
    deleteStudent() {},
  },
};
</script>

<style lang="scss" scoped>
@import "@/assets/styles/common.scss";

.student {
  position: relative;
  width: 100%;
  display: grid;
  grid-template-columns: 1fr 40px 40px;
  grid-template-areas: "text edit delete";
  border-bottom: $border-default;
  @include setProperty(padding, 8px, 10px 12px, 12px 16px, 12px 18px);

  &:last-child {
    border-bottom: none;
  }

  @include xs {
    padding-right: 12px;
  }

  @include sm {
    grid-template-columns: 1fr 50px 50px;

    &:first-child {
      border-radius: $common-corner $common-corner 0 0;
    }

    &:last-child {
      border-radius: 0 0 $common-corner $common-corner;
    }
  }

  @include md {
    grid-template-columns: 1fr 60px 60px;
  }
}

.student--loading:after {
  content: "";
  position: absolute;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  user-select: none;
  background: rgba(#dedede, 0.5);
}

.student__data {
  width: 100%;
  grid-area: text;
  text-align: left;
  display: grid;
  grid-template-rows: 1fr 1fr;
  align-content: center;
  gap: 8px;
}

.student__name,
.student__passport {
  overflow: hidden;
  width: 100%;
  text-overflow: ellipsis;
  white-space: nowrap;
  @include setProperty(height, 26px, 28px, 32px, 32px);
  @include setProperty(line-height, 26px, 28px, 32px, 32px);

  input {
    width: 100%;
    max-width: 600px;
    height: 100%;
    font-size: 14px;
    padding-left: 4px;
    padding-right: 4px;
    border-radius: 6px;
  }
}

.student__name {
  font-size: 16px;
  font-weight: bold;
}

.student__passport {
  font-size: 12px;
  color: #727272;
}

.student__edit,
.student__delete {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;

  & a {
    text-decoration: none;
    cursor: pointer;
    border-radius: $common-corner;
    border: $border-default;
    display: block;
    width: 28px;
    height: 28px;
    background-size: 50%;
    background-repeat: no-repeat;
    background-position: center;
    user-select: none;

    @include sm {
      width: 36px;
      height: 36px;

      &:hover {
        background-color: rgba(#ddd, 0.3);
      }
    }
  }
}

.student__edit a {
  grid-area: edit;
  background-image: url("@/assets/icons/edit.svg");
}

.student__edit--save a {
  background-image: url("@/assets/icons/check.svg");
}

.student__delete a {
  grid-area: delete;
  background-image: url("@/assets/icons/delete.svg");
}

.student__edit--cancel a {
  background-image: url("@/assets/icons/cancel.svg");
}
</style>
