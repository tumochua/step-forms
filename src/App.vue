<template>
  <div id="app">
    <ProgressBarVue :state="state" />
    <HeaderVue :state="state" />
    <FormValidationVue
      :state="state"
      @changeInput="changeInput"
      @handleNext="handleNext"
      @handlePrevious="handlePrevious"
      @handleRest="handleRest"
    />
  </div>
</template>

<script>
import ProgressBarVue from "./components/ProgressBar.vue";
import HeaderVue from "./components/Header.vue";
import FormValidationVue from "./components/stepForm/FormValidation.vue";
import { mapState, mapGetters } from "vuex";
export default {
  name: "App",
  components: {
    ProgressBarVue,
    HeaderVue,
    FormValidationVue,
  },
  data() {
    return {
      state: {
        currentStep: 1,
        formStep: [
          {
            stepId: 1,
            stepName: "About you",
            success: false,
            listField: {
              name: {
                value: "",
                label: "Full Name",
                type: "text",
                error: false,
                message: "",
              },
              email: {
                value: "",
                label: "Your Email",
                type: "email",
                error: false,
                message: "",
              },
            },
          },
          {
            stepId: 2,
            stepName: "About Your Company",
            success: false,
            listField: {
              company: {
                value: "",
                label: "Your Company Name",
                type: "text",
                error: false,
                message: "",
              },
              numberEmployees: {
                value: "",
                label: "Number of Employees",
                type: "number",
                error: false,
                message: "",
              },
            },
          },
          {
            stepId: 3,
            stepName: "Finishing Up",
            success: false,
            listField: {
              connectUs: {
                value: "",
                label: "From Where did you hear about us?",
                type: "select",
                validate() {
                  if (this.value.length <= 0) {
                    this.error = true;
                    this.message = "The field is required!";
                  } else {
                    this.error = false;
                    this.message = "";
                  }
                },
                selectTitle: "-- Choose answer --",
                optionData: ["Friend", "FaceBook", "Websites"],
                error: false,
                message: "",
              },
              terms: {
                value: false,
                label: "",
                type: "checkbox",
                title: "I accept terms & conditions",
                validate() {
                  if (!this.value) {
                    this.error = true;
                    this.message = "The field is required!";
                    return;
                  } else {
                    this.error = false;
                    this.message = "";
                  }
                },
                error: true,
                message: "",
              },
            },
          },
        ],
      },
    };
  },
  computed: {
    ...mapState({}),
    ...mapGetters([""]),
  },

  methods: {
    handleNext() {
      if (this.state.currentStep === 3) {
        return;
      }

      if (this.state.currentStep === 1) {
        this.valiDationForm1();
        return;
      }
      if (this.state.currentStep === 2) {
        this.valiDationForm2();
        return;
      }
    },
    handlePrevious() {
      if (this.state.currentStep === 1) {
        return;
      }
      this.state.currentStep--;
    },

    valiDationForm1() {
      const form = this.state.formStep[this.state.currentStep - 1];
      const name = form.listField.name.value;
      const email = form.listField.email.value;
      if (!name) {
        form.listField.name.message = "The field is required!";
      } else {
        form.listField.name.message = "";
      }
      if (!email) {
        form.listField.email.message = "The field is required!";
        return;
      } else {
        form.listField.email.message = "";
      }
      const validationEmail = /^[a-zA-Z0-9.]+@+[a-zA-Z0-9]+.+[A-z]/.test(email);
      if (!validationEmail) {
        form.listField.email.message = "The field must be email!";
      } else {
        form.listField.email.message = "";
      }

      if (!name || !email || !validationEmail) {
        return;
      } else {
        this.state.currentStep++;
        return;
      }
    },

    valiDationForm2() {
      const form = this.state.formStep[this.state.currentStep - 1];
      const company = form.listField.company.value;
      const numberEmployees = form.listField.numberEmployees.value;

      if (!company) {
        form.listField.company.message = "The field is required!";
      } else {
        form.listField.company.message = "";
      }
      if (!numberEmployees) {
        form.listField.numberEmployees.message = "The field is required!";
      } else {
        form.listField.numberEmployees.message = "";
      }

      if (!company && !numberEmployees) {
        return;
      } else {
        this.state.currentStep++;
      }
    },
    // valiDationForm3() {
    //   this.state.currentStep++;
    //   return;
    // },
    handleRest() {
      this.state.currentStep = 1;
      this.state.formStep[0].listField.name.value = "";
      this.state.formStep[0].listField.email.value = "";
      this.state.formStep[1].listField.company.value = "";
      this.state.formStep[1].listField.numberEmployees.value = "";
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 20px;
  width: 990px;
  margin: 0 auto;
}
</style>
