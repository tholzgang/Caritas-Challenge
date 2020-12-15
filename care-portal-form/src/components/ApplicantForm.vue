<template>
  <section>
    <div class="container">
      <div class="field">
        <h5>Have you taken a care course or nursing course?</h5>
        <b-switch v-model="hasCourse">
          <label>{{ getLabel(hasCourse) }}</label>
        </b-switch>
      </div>

      <div class="field" v-if="hasCourse">
        <p>How long was the course?</p>
        <b-field label="(Hours)">
          <b-slider v-model="timeCourse" :max="40">
            <template v-for="val in [2, 10, 20, 40]">
              <b-slider-tick :value="val" :key="val">{{ val }}</b-slider-tick>
            </template>
          </b-slider>
        </b-field>
      </div>

      <div class="field">
        <h5>Do you have experience in caring for older people?</h5>
        <b-switch v-model="hasOlder">
          <label>{{ getLabel(hasOlder) }}</label>
        </b-switch>
      </div>
      <div class="field" v-if="hasOlder">
        <p>What length of experience?</p>
        <b-field label="(Years)">
          <b-slider v-model="timeOlder" :min="0" :max="25"></b-slider>
        </b-field>
      </div>

      <h5>Experience in special care</h5>
      <div class="field">
        <p>Select all that apply</p>
        <div class="field">
          <b-checkbox v-model="chkSpecial.dem">Dementia</b-checkbox>
          <b-checkbox v-model="chkSpecial.mha">Mental handicap</b-checkbox>
          <b-checkbox v-model="chkSpecial.str">Stroke</b-checkbox>
        </div>
      </div>
      <h5>Experience with assistive devices</h5>
      <div class="field">
        <p>Select all that apply</p>
        <div class="field">
          <b-checkbox v-model="chkDevice.rol">Rollator</b-checkbox>
          <b-checkbox v-model="chkDevice.whe">Wheelchair</b-checkbox>
          <b-checkbox v-model="chkDevice.pac">Pacemaker</b-checkbox>
        </div>
      </div>
      <h5>German proficiency</h5>
      <div class="field">
        <b-select placeholder="Select level" v-model="levelGerman">
          <option
            v-for="option in profGerman"
            :value="option.id"
            :key="option.id"
          >
            {{ option.txt }}
          </option>
        </b-select>
      </div>
      <h5>Get my results</h5>
      <button
        :disabled="salaryPreview == 500"
        class="button is-primary"
        @click="isResultShown = true"
      >
        Click here to estimate salary range
      </button>
    </div>

    <b-modal v-model="isResultShown">
      <div class="container">
        <div class="modal-card" style="width: auto">
          <header class="modal-card-head">
            <p class="modal-card-title">Results</p>
          </header>
          <section class="modal-card-body">
            <p>Based on your inputs, we have calculated your salary to be:</p>
            <h1>{{ salaryPreview }} CHF</h1>
            <p>
              For more information and support, share your e-mail address to be
              contacted by our staff:
            </p>
            <form
              action="https://formspree.io/f/{form_id}"
              method="post"
              target="_blank"
            >
              <b-field>
                <b-input
                  type="email"
                  name="email"
                  placeholder="Your email"
                  required
                >
                </b-input>
                <button class="button is-primary">Send</button>
              </b-field>
            </form>
          </section>
        </div>
      </div>
    </b-modal>
  </section>
</template>

<script>
export default {
  name: "ApplicantForm",
  data() {
    return {
      hasCourse: false,
      timeCourse: 0,
      hasOlder: false,
      timeOlder: 0,
      chkDevice: {},
      chkSpecial: {},
      levelGerman: 0,
      profGerman: [
        { id: 0, txt: "None" },
        { id: 1, txt: "B1 Intermediate" },
        { id: 2, txt: "B2 Good competence" },
        { id: 3, txt: "C1 Very good" },
      ],
      isResultShown: false,
    };
  },
  computed: {
    salaryPreview() {
      return (
        500 +
        this.timeCourse * 20 +
        this.timeOlder * 50 +
        this.levelGerman * 100 +
        50 * Object.keys(this.chkDevice).filter((k, i) => k).length +
        50 * Object.keys(this.chkSpecial).filter((k, i) => k).length
      );
    },
  },
  methods: {
    getLabel(val) {
      return val ? "Yes" : "No";
    },
  },
};
</script>

<style scoped>
.field {
  margin: 1em 2em;
}
h5 {
  display: block;
  font-size: 125%;
  border-top: 1px solid #ccc;
  margin-top: 2em;
  padding-top: 1em;
}
p {
  font-weight: bolder;
}
.modal-card-body p {
  font-weight: normal;
  text-align: left;
}
.modal-card-body h1 {
  margin: 1em;
  font-size: 150%;
}
</style>