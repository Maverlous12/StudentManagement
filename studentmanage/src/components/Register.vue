<template>
  <div>
    <b-button class="btn-add" v-b-modal.modal-prevent-closing
      >Add More</b-button
    >
    <b-button class="btn-add" @click="handleDeleteAll">Delete All</b-button>

    <b-modal
      id="modal-prevent-closing"
      ref="modal"
      title="Information"
      @show="resetModal"
      @hidden="resetModal"
      @ok="handleOk"
    >
      <form ref="form" @submit.stop.prevent="handleSubmit">
        <b-form-group label="Name">
          <b-form-input v-model="student.name"></b-form-input>
        </b-form-group>
        <b-form-group label="Age">
          <b-form-input v-model="student.age"></b-form-input>
        </b-form-group>
        <b-form-group label="Class">
          <b-form-input v-model="student.class"></b-form-input>
        </b-form-group>
        <b-form-group label="Address">
          <b-form-input v-model="student.address"></b-form-input>
        </b-form-group>
      </form>
    </b-modal>
  </div>
</template>

<script>
export default {
  props: {
    user: {
      type: Object,
    },
  },
  watch: {
    user() {
      if (this.user) {
        this.student = Object.assign({}, this.user);
      } else {
        this.student = {};
      }
    },
  },
  data() {
    return {
      student: {
        id: Math.floor(Math.random() * 100),
        name: '',
        age: '',
        class: '',
        address: '',
      },
    };
  },
  methods: {
    checkFormValidity() {
      const valid = this.$refs.form.checkValidity();
      this.nameState = valid;
      return valid;
    },
    resetModal() {
      this.name = '';
      this.nameState = null;
    },
    handleOk(bvModalEvt) {
      // Prevent modal from closing
      bvModalEvt.preventDefault();
      this.handleSubmit();
      //   // Trigger submit handler
      //   this.handleSubmit();
      //   console.log(this.student);
      this.$emit('save', this.student);
      this.student = {
        id: Math.floor(Math.random() * 100),
        name: '',
        age: '',
        class: '',
        address: '',
      };
    },
    handleSubmit() {
      // Exit when the form isn't valid
      if (!this.checkFormValidity()) {
        return;
      }
      this.$nextTick(() => {
        this.$bvModal.hide('modal-prevent-closing');
      });
    },
    handleDeleteAll() {
      this.$emit('deleteAll');
    },
  },
};
</script>

<style>
.btn-add {
  margin-top: 10px;
  margin-left: 5px;
}
</style>
