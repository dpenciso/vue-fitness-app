<template>
  <div id="workoutList-table">
    <p v-if="workouts.length < 1">No Workouts</p>
    <table v-else>
      <thead>
        <tr>
          <th>Workout</th>
          <th>Weight</th>
          <th>Reps</th>

          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="workout in workouts" :key="workout.id">
          <td v-if="editing === workout.id">
            <input v-model="workout.name" type="text" />
          </td>
          <td v-else>{{ workout.name }}</td>
          <td v-if="editing === workout.id">
            <input v-model="workout.weight" type="text" />
          </td>
          <td v-else>{{ workout.weight }}</td>
          <td v-if="editing === workout.id">
            <input v-model="workout.reps" type="text" />
          </td>
          <td v-else>{{ workout.reps }}</td>
          <td v-if="editing === workout.id">
            <button @click="editWorkout(workout)">Save</button>
            <button class="muted-button" @click="cancelEdit(workout)">
              Cancel
            </button>
          </td>
          <td v-else>
            <button @click="editMode(workout)">Edit</button>
            <button @click="$emit('delete:workout', workout.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "WorkoutList",
  props: {
    workouts: Array,
  },
  data() {
    return {
      editing: null,
      cachedWorkout: null,
    };
  },
  methods: {
    editMode(workout) {
      this.cachedWorkout = Object.assign({}, workout);
      this.editing = workout.id;
    },
    editWorkout(workout) {
      if (workout.name === "" || workout.reps === "") return;

      this.$emit("edit:workout", workout.id, workout);
      this.editing = null;
    },
    cancelEdit(workout) {
      Object.assign(workout, this.cachedWorkout);
      this.editing = null;
    },
  },
};
</script>

<style>
</style>