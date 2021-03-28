<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <div>
        <label>Workout Name <sup>*</sup></label>
        <input
          v-model="workout.name"
          type="text"
          :class="{ 'has-error': submitting && invalidName }"
          @focus="clearStatus"
        />
      </div>
      <div>
        <label>Time</label>
        <input v-model="workout.time" type="text" @focus="clearStatus" />
      </div>
      <div>
        <label>Weight</label>
        <input v-model="workout.weight" type="number" @focus="clearStatus" />
      </div>
      <div>
        <label>Number of Sets</label>
        <input v-model="workout.sets" type="number" @focus="clearStatus" />
      </div>
      <div>
        <label>Number of Reps</label>
        <input v-model="workout.reps" type="number" @focus="clearStatus" />
      </div>
      <div>
        <label>Date</label>
        <input type="date" v-model="workout.date" @focus="clearStatus" />
      </div>
      <div>
        <button class="addButton">Add Workout</button>
        <p v-if="error && submitting" class="error-message">
          Please fill out all required fields
        </p>
        <p v-if="success" class="success-message">Workout successfully added</p>
      </div>
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
      if (this.invalidName) {
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
        date: new Date().toISOString().substr(0, 10),
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
  },
};
</script>

<style>
* {
  color: rgb(166, 255, 0);
}

form {
  margin-bottom: 2rem;
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
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

sup {
  color: red;
}
</style>