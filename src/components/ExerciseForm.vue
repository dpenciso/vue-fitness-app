<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <label>Workout Name</label>
      <input
        v-model="workout.name"
        type="text"
        :class="{ 'has-error': submitting && invalidName }"
        @focus="clearStatus"
      />
      <label>Weight</label>
      <input
        v-model="workout.weight"
        type="number"
        :class="{ 'has-error': submitting && invalidWeight }"
        @focus="clearStatus"
      />
      <label>Number of Reps</label>
      <input
        v-model="workout.reps"
        type="number"
        :class="{ 'has-error': submitting && invalidReps }"
        @focus="clearStatus"
      />
      <button>Add Workout</button>
      <p v-if="error && submitting" class="error-message">
        Please fill out all required fields
      </p>
      <p v-if="success" class="success-message">Workout successfully added</p>
    </form>
  </div>
</template>

<script>
export default {
  name: "exercise-form",
  data() {
    return {
      workout: {
        name: "",
        weight: "",
        reps: "",
      },
      submitting: false,
      error: false,
      success: false,
    };
  },
  methods: {
    handleSubmit() {
      this.submitting = true;
      this.clearStatus();

      if (this.invalidName || this.invalidReps || this.invalidWeight) {
        this.error = true;
        return;
      }

      this.$emit("add:workout", this.workout);
      this.workout = {
        name: "",
        weight: "",
        reps: "",
      };

      this.error = false;
      this.success = true;
      this.submitting = false;
    },
    clearStatus() {
      this.success = false;
      this.error = false;
    },
  },
  computed: {
    invalidName() {
      return this.workout.name.trim() === "";
    },
    invalidWeight() {
      return this.workout.weight.trim() === "";
    },
    invalidReps() {
      return this.workout.reps.trim() === "";
    },
  },
};
</script>

<style>
form {
  margin-bottom: 2rem;
}

[class*+'-message'] {
  font-weight: 500;
}

.error-message {
  color: red;
}

.success-message {
  color: green;
}
</style>