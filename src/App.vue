<template>
  <div id="app" class="small-container">
    <h1>Workout List</h1>
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
          name: "push-ups",
          weight: 100,
          reps: 15,
        },
        {
          id: 2,
          name: "sit-ups",
          weight: 50,
          reps: 50,
        },
        {
          id: 3,
          name: "pull-ups",
          weight: 30,
          reps: 10,
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
}

.small-container {
  max-width: 680px;
}
</style>
