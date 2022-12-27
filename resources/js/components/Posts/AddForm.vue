<template>
  <div class="row d-flex justify-content-center">
    <div class="col-10">
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
      <div class="d-flex gap-2">
        <Button
          :btnType="'save'"
          :btnTxt="'Guardar'"
          :btnAction="save"
        ></Button>
        <Button
          :btnType="'cancel'"
          :btnTxt="'Cancelar'"
          :btnAction="cancel"
        ></Button>
      </div>

    </div>
  </div>

</template>

<script>
import FormInput from "../Forms/Input.vue";
import Button from "../Forms/Btn.vue";
import TxtArea from "../Forms/TxtArea.vue";
import Swal from "sweetalert2";

import axios from "axios";
export default {
  components: {
    FormInput,
    Button,
    TxtArea,
  },
  emits: ["newPost", "hideForm"],
  data() {
    return {
      title: "",
      description: "",
      strings: {
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
        Swal.fire({
          title: "¡Hey!",
          text: "Datos incompletos.",
          icon: "warning",
        });
        return;
      }

      axios
        .post("/api/posts", {
          title: this.title,
          description: this.description,
        })
        .then((r) => {
          this.clear();

          this.$emit("newPost", "reload");
          Swal.fire({
            title: "¡Listo!",
            text: "Se ha agregado el post con éxito.",
            icon: "success",
          });
        })
        .catch((e) => {
          Swal.fire({
            title: "¡Ooops!",
            text: "Ha habido un error al guardar el post :(.",
            icon: "error",
          });
        });
    },
    clear() {
      this.title = "";
      this.description = "";
    },
    cancel() {
      this.$emit("hideForm", true);
    },
  },
};
</script>

<style>
ul {
  padding-inline-start: 0px;
}
</style>
