<template>
  <div>
    <h1>Simple form</h1>
    <ul v-if="this.error.length > 0">
      <li v-for="item in this.error" v-bind:key="item">Invalid {{ item }}</li>
    </ul>
    <form>
      <div class="form">
        <label for="name">Full name:</label>
        <input
          type="text"
          id="name"
          placeholder="enter name"
          v-model="form.name"
        />
      </div>
      <div class="form">
        <label for="email">Email:</label>
        <input
          type="email"
          id="email"
          placeholder="enter email"
          v-model="form.email"
        />
      </div>
      <div class="form">
        <label for="password">Password:</label>
        <input
          type="password"
          id="password"
          placeholder="enter password"
          v-model="form.password"
        />
      </div>
      <div class="form">
        <label for="gender">Gender:</label>
        <input
          type="radio"
          name="gender"
          value="male"
          v-model="form.gender"
        />Male
        <input
          type="radio"
          name="gender"
          value="female"
          v-model="form.gender"
        />Female
        <input
          type="radio"
          name="gender"
          value="other"
          v-model="form.gender"
        />Other
      </div>
      <div class="form">
        <label for="country">Country:</label>
        <select id="country" v-model="form.country">
          <option value="nepal" selected>Nepal</option>
          <option value="us">USA</option>
          <option value="india">India</option>
          <option value="canada">Canada</option>
          <option value="other">Other</option>
        </select>
      </div>
      <div class="form-group">
        <h3>Technology</h3>
        <label for="java">Java</label>
        <input
          type="checkbox"
          id="java"
          value="java"
          v-model="form.technology"
        />
        <br />
        <label for="python">Python</label>
        <input
          type="checkbox"
          id="python"
          value="python"
          v-model="form.technology"
        />
        <br />
        <label for="js">JavaScript</label>
        <input
          type="checkbox"
          id="js"
          value="javascript"
          v-model="form.technology"
        />
        <br />
        <label for="dotnet">Dot net</label>
        <input
          type="checkbox"
          id="dotnet"
          value="dotnet"
          v-model="form.technology"
        />
        <br />
        <label for="blockchain">Blockchain</label>
        <input
          type="checkbox"
          id="blockchain"
          value="blockchain"
          v-model="form.technology"
        />
      </div>
      <button v-on:click.prevent="submit" type="submit" class="btn">Submit</button>
    </form>
  </div>
</template>
<script>
export default {
  name: "App",
  data() {
    return {
      form: {
        name: "",
        email: "",
        password: "",
        gender: "",
        country: "",
        technology: [],
      },
      error: [],
    };
  },
  methods: {
    submit() {
  this.error = [];
  // Checks for empty fields
  for (const item in this.form) {
    if (this.form[item] === "" || this.form[item].length === 0) {
      this.error.push(item);
    }
  }
  // Stop validation if there are empty fields
  if (this.error.length > 0)
   return;

  // Validate name
  if (!/^[a-zA-Z]+\s[a-zA-Z]+$/.test(this.form.name)) {
    this.error.push("name");
    return; // Stop validation if name is invalid
  }
  // Validate password
  if (!/(?=.*[A-Z])(?=.*[a-z])(?=.*[0-9])(?=.*[\W_])/.test(this.form.password)) {
    this.error.push("password");
    return; // Stop validation if password is invalid
  }

  // Validate email (using a more comprehensive regex)
  if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(this.form.email)) {
    this.error.push("email");
    return; // Stop validation if email is invalid
  }

  // If no errors, submit data
  if (this.error.length === 0) {
    alert("Data Submitted");
  }
},


  },
};
</script>
<style>
.form {
  margin: 10px 10px;
}
.form label {
  display: flex;
}
.btn {
  margin: 10px;
  padding: 5px;
  letter-spacing: 1px;
  color: #fff;
  background-color: #333;
  border: none;
  border-radius: 3px;
}
.form-group {
  margin: 10px 10px;
}
</style>
