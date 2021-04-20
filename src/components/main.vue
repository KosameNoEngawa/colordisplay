<template>
  <div id="main-wrapper">
    <div class="d-flex flex-column bd-highlight mb-3">
    <b-form-group id="input-group-color-one">
      <b-form-select
      id="input-color-one"
      v-model="main_data.color_one"
      :options="colors"
      required>
      </b-form-select>
    </b-form-group>
    <b-button v-on:click="add_color_two" class="p-2 bd-highlight" v-bind:style="button">色2を追加</b-button>
    <b-form-group id="input-group-color-two" v-show='two_add_success'>
      <b-form-select
      id="input-color-two"
      v-model="main_data.color_two"
      :options="colors"
      required>
      </b-form-select>
    </b-form-group>
    <b-button v-on:click="add_color_three" class="p-2 bd-highlight" v-bind:style="button">色３を追加</b-button>
    <b-form-group id="input-group-color-three" v-show='three_add_success'>
      <b-form-select
      id="input-color-three"
      v-model="main_data.color_three"
      :options="colors"
      required>
      </b-form-select>
    </b-form-group>
    <b-button v-on:click="submit_color" class="p-2 bd-highlight">表示</b-button>
    </div>
    <transition id="color_varidation">
      <b-alert v-show='color_validation' variant="nothing" class="button" show>色を選んでください</b-alert>
    </transition>
    <div id="color-palette" v-bind:style="styles">
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
    </div>
    <div id="test-color">
      <br>
    </div>
  </div>
</template>

<script>

export default {
  name: 'main-wrapper',
  data() {
    return {
      main_data: {
        color_one: ["0","0","0"],
        color_two: ["0","0","0"],
        color_three: ["0","0","0"],
        display_color: ["0","0","0"],
        test: "rgb(255,0,0)"
      },
      colors: [{ text: "none", value: ["0","0","0"]}, { text: "blue", value: ["0","0","255"] }, { text: "red", value: ["255", "0", "0"]}, { text: "green", value: ["0","255","0"]}],
      styles: {
        backgroundColor: "",
      },
      color_validation: false,
      two_add_success: false,
      three_add_success: false,
      button: {
        margin: "20px 50px",
      }
    }
  },
  methods: {
    submit_color: function() {
      if(this.main_data.color_one == "" && this.main_data.color_two == "") {
        this.color_validation = true;
        setTimeout(function(){this.color_validation = false;}.bind(this), 700);
      }
        this.main_data.display_color[0] = this.main_data.color_one[0] + this.main_data.color_two[0] + this.main_data.color_three[0];
        this.main_data.display_color[1] = this.main_data.color_one[1] + this.main_data.color_two[1] + this.main_data.color_three[1];
        this.main_data.display_color[2] = this.main_data.color_one[2] + this.main_data.color_two[2] + this.main_data.color_three[2];
        this.styles.backgroundColor = "rgba("+this.main_data.display_color[0]+","+this.main_data.display_color[1]+","+this.main_data.display_color[2]+")";
    },
    add_color_three: function() {
      this.three_add_success = true;
    },
    add_color_two: function() {
      this.two_add_success = true;
    },
  }
}
</script>

<style>
#main-wrapper {
  margin: 0 auto;
}
#color-palette {
  border: 1px solid#333333;
}
</style>