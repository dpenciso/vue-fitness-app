<template>
  <div id="app" class="small-container">
    <h1>Workout Tracker</h1>
    <exercise-form @add:workout="addWorkout" />
    <workout-list
      :workouts="workouts"
      @delete:workout="deleteWorkout"
      @edit:workout="editWorkout"
    />
  </div>
</template>

<script>
import ExerciseForm from "./components/ExerciseForm.vue";
import WorkoutList from "./components/WorkoutList.vue";

export default {
  name: "App",
  components: {
    WorkoutList,
    ExerciseForm,
  },
  data() {
    return {
      workouts: [
        {
          id: 1,
          name: "run",
          time: "14:00",
          weight: "",
          sets: "",
          reps: "",
          date: "2021-03-23",
        },
        {
          id: 2,
          name: "sit-ups",
          time: "",
          weight: "",
          sets: 3,
          reps: 50,
          date: "2021-03-23",
        },
        {
          id: 3,
          name: "bench press",
          time: "",
          weight: 150,
          sets: 5,
          reps: 10,
          date: "2021-03-23",
        },
      ],
    };
  },
  methods: {
    addWorkout(workout) {
      const lastId =
        this.workouts.length > 0
          ? this.workouts[this.workouts.length - 1].id
          : 0;

      const id = lastId + 1;

      const newWorkout = { ...workout, id };

      this.workouts = [...this.workouts, newWorkout];
    },
    deleteWorkout(id) {
      this.workouts = this.workouts.filter((workout) => workout.id !== id);
    },
    editWorkout(id, updatedWorkout) {
      this.workouts = this.workouts.map((workout) =>
        workout.id === id ? updatedWorkout : workout
      );
    },
  },
};
</script>

<style>
button {
  background: green;
  border: 1px solid green;
  margin: 1rem;
}

button:hover {
  background: rgba(0, 128, 0, 0.5);
  border: 1px solid rgba(0, 128, 0, 0.5);
}

.small-container {
  max-width: 760px;
}

* body {
  background-color: rgb(50, 50, 50);
  color: rgb(166, 255, 0);
}

h1 {
  color: rgb(166, 255, 0);
}
</style>
