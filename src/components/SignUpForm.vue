<template>
  <form>

    <label>Email:</label>
    <input type="email"
           aria-label="Email"
           v-model="email"
           required
    />

    <label>Password:</label>
    <input type="password"
           aria-label="Password"
           v-model="password"
           required
    />

    <label>Role:</label>
    <select aria-label="Role"
            v-model="role"
            required
    >
      <option value="Developer">Developer</option>
      <option value="Designer">Designer</option>
    </select>

    <label>Skills:</label>
    <input type="text"
           aria-label="Skills"
           v-model="tempSkill"
           @keyup.alt="addSkill"
    >
    <ul class="skills">
      <li v-for="(skill, index) in skills"
          :key="index"
          @click="deleteSkill(index)"
          class="pill"
          style="cursor: not-allowed;"
      >
        {{ skill }}
      </li>
    </ul>

    <div class="terms">
      <input type="checkbox" aria-label="Accept" v-model="terms" required>
      <label>Accept terms and conditions</label>
    </div>

  </form>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      role: 'Developer',
      terms: true,
      tempSkill: '',
      skills: [],
    }
  },
  methods: {
    addSkill(event) {
      if (event.key === ',' && !this.skills.includes(this.tempSkill)) {
        this.skills.push(this.tempSkill);
        this.tempSkill = '';
      }
    },
    deleteSkill(index) {
      this.skills.splice(index, 1);
    }
  }
}
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}

label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}

input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}

.terms {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  padding-top: 20px;
}

.terms input {
  width: auto;
}

.terms label {
  margin: 0 0 0 15px;
}
</style>
