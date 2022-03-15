<template>
  <div>
    <div v-for="post in posts" v-bind:key="post.id">
      <h2>{{ post }}</h2>
    </div>
    <select
      name="LeaveType"
      @change="onChange($event)"
      class="form-control"
      v-model="key"
    >
      <option value="1">Annual Leave/ Off-Day</option>
      <option value="2">On Demand Leave</option>
    </select>
  </div>
</template>

<script>
export default {
  data() {
    return {
      posts: [],
      key: "1",
    };
  },

  methods: {
    async getData() {
      try {
        let response = await fetch("https://localhost:7228/api/Bart");
        // JSON responses are automatically parsed.
        this.posts = await response.json();
      } catch (error) {
        console.log(error);
      }
    },
    onChange(event) {
      console.log(event.target.value);
    },
  },
  created() {
    this.getData();
  },
};
</script>
