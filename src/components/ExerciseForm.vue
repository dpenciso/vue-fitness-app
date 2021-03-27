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
      <label>Time</label>
      <input
        v-model="workout.time"
        type="text"
        :class="{ 'has-error': submitting && invalidTime }"
        @focus="clearStatus"
      />
      <label>Weight</label>
      <input
        v-model="workout.weight"
        type="number"
        :class="{ 'has-error': submitting && invalidWeight }"
        @focus="clearStatus"
      />
      <label>Number of Sets</label>
      <input
        v-model="workout.sets"
        type="number"
        :class="{ 'has-error': submitting && invalidSets }"
        @focus="clearStatus"
      />
      <label>Number of Reps</label>
      <input
        v-model="workout.reps"
        type="number"
        :class="{ 'has-error': submitting && invalidReps }"
        @focus="clearStatus"
      />
      <label>Date</label>
      <input
        type="date"
        v-model="workout.date"
        :class="{ 'has-error': submitting && invalidDate }"
        @focus="clearStatus"
      />
      <button class="addButton">Add Workout</button>
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
        time: "",
        weight: "",
        sets: "",
        reps: "",
        date: new Date().toISOString().substr(0, 10),
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

      if (
        this.invalidName ||
        this.invalidReps ||
        this.invalidWeight ||
        this.invalidDate ||
        this.invalidSets ||
        this.invalidTime
      ) {
        this.error = true;
        return;
      }

      this.$emit("add:workout", this.workout);
      this.workout = {
        name: "",
        time: "",
        weight: "",
        sets: "",
        reps: "",
        date: "",
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
    invalidTime() {
      return this.workout.reps.trim() === "";
    },
    invalidWeight() {
      return this.workout.weight.trim() === "";
    },
    invalidSets() {
      return this.workout.sets.trim() === "";
    },
    invalidReps() {
      return this.workout.reps.trim() === "";
    },
  },
};
</script>

<style>
* {
  color: rgb(166, 255, 0);
}

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
  color: rgb(166, 255, 0);
}

.addButton {
  margin-left: 0;
}
</style>