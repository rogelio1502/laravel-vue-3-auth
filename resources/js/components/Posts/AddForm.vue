<template>
  <div>
    <Alert
      :alertTxt="alertTxt"
      :type="alertType"
      v-show="submitOk"
    ></Alert>
    <FormInput
      :inputId="'ipt-title'"
      :inputLabel="'Titulo del Post'"
      :inputType="'text'"
      v-model="title"
    ></FormInput>
    <TxtArea
      :inputId="'ipt-desc'"
      :inputLabel="'Descripción'"
      v-model="description"
    ></TxtArea>
    <Button
      :btnType="'save'"
      :btnTxt="'Guardar'"
      :btnAction="save"
    ></Button>
  </div>
</template>

<script>
import FormInput from "../Forms/Input.vue";
import Button from "../Forms/Btn.vue";
import Alert from "../Forms/Alert.vue";
import TxtArea from "../Forms/TxtArea.vue";


import axios from "axios";
export default {
  components: {
    FormInput,
    Button,
    Alert,
    TxtArea,
  },
  data() {
    return {
      title: "",
      description: "",
      submitOk: false,
      alertTxt: "",
      alertType: "",
      strings = {
        success: {
            txt: "El post ha sido guardado correctamente.",
            type: "success",
        },
        incomplete: {
            txt: "Datos incompletos.",
            type: "warning",
        },
        error: {
            txt: "Error al guardar.",
            type: "danger",
        },
     },
    };
  },
  methods: {
    save() {
      if (this.title == "" || this.description == "") {
        this.alertTxt = strings.incomplete.txt;
        this.alertType = strings.incomplete.type;
        this.showAlert();
        return;
      }

      axios
        .post("/api/posts", {
          title: this.title,
          description: this.description,
        })
        .then((r) => {
          console.log(r);
          this.clear();
          this.alertTxt = strings.success.txt;
          this.alertType = strings.success.type;
          this.showAlert();
        })
        .catch((e) => {
          console.log(e);
          this.alertTxt = strings.error.txt;
          this.alertType = strings.error.type;
          this.showAlert();
        });
    },
    clear() {
      this.title = "";
      this.description = "";
    },
    showAlert() {
      this.submitOk = true;
    },
  },
};
</script>

<style>
</style>
