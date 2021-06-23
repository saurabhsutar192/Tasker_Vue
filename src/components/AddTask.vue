<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <input type="text" v-model="text" name="text" placeholder="Add Task" />
    </div>

    <div class="form-control form-control-check">
      <label>Set Reminder</label>
      <input type="checkbox" v-model="reminder" name="reminder" />
    </div>

    <input type="submit" value="Save Task" class="btn btn-block save" />
  </form>
</template>

<script>
export default {
  name: "AddTask",
  data() {
    return {
      text: "",

      reminder: false,
    };
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();

      if (!this.text) {
        alert("Please add a task");
        return;
      }

      const newTask = {
        text: this.text,

        reminder: this.reminder,
      };

      this.$emit("add-task", newTask);

      this.text = "";
      this.day = "";
      this.reminder = false;
    },
  },
};
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
  width: 100vw;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.form-control {
  margin: 20px 0;
}

.form-control label {
  display: block;
  font-size: 20px;
}

.form-control input {
  width: 60vw;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
  border-radius: 20px;
  border: 1px solid #3d405b;
  text-align: center;
  outline: none;
}

.form-control-check {
  width: 60vw;
  display: flex;
  align-items: center;

  justify-content: center;
}

.btn {
  background: #81b29a;
  border: none;
  padding: 20px;
  color: white;
  cursor: pointer;
}

.form-control-check input {
  width: 20px;
  height: 20px;
  margin: 2vh;
  cursor: pointer;
}
</style>
