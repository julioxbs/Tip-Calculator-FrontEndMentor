<template>
  <div class="calculator row align-items-center justify-content-center">
    <div class="left-side col-10 col-sm-8 col-lg-6 ">
      <form class="d-flex flex-column gap-3">
        <div class="d-flex flex-column my-2">
          <label class="bill">Bill</label>
          <input
            type="number"
            style="background-color: var(--clr-lighter-grayish-cyan)"
            placeholder="0"
            class="form-control"
            v-model="billValue"
            max="11"
            min="1"
          />
        </div>

        <div class="select-tips">
          <label class="mb-2">Select Tip %</label>
          <div class="d-flex flex-wrap gap-1 mb-2">
            <a href="#" class="btn btn-tips" @click="getValue">5%</a>
            <a href="#" class="btn btn-tips" @click="getValue">10%</a>
            <a href="#" class="btn btn-tips" @click="getValue">15%</a>
            <a href="#" class="btn btn-tips" @click="getValue">20%</a>
            <a href="#" class="btn btn-tips" @click="getValue">25%</a>
            <input v-if="billValue != ''" type="number" v-model="customTip" placeholder="Custom" class="form-control" min="1" max="100" style="width: 27%" @input="calCustom" />
            <input v-else type="number" v-model="customTip" placeholder="Custom" class="form-control" min="1" max="100" style="width: 27%" disabled />
          </div>
        </div>

        <div class="d-flex flex-column">
          <label class="number-people">Number of People</label>
          <input v-if="billValue != ''" type="number" placeholder="0" class="form-control" v-model="people" />
          <input v-else type="number" placeholder="0" class="form-control" v-model="people" disabled />
        </div>
      </form>
    </div>

    <div class="right-side col-lg-6 p-3">
        <div class="d-flex justify-content-between align-items-center">
            <p class="tip d-flex flex-column">
                Tip Amount
                <span class="person"> {{valueTip}} / Person</span>
            </p>

            <span class="val">${{ resultTip === "" ? "0.00" : resultTip }}</span>
        </div>

        <div class="d-flex justify-content-between align-items-center">
            <p class="tip d-flex flex-column">
                Total Person
                <span class="person">{{people}} / Person</span>
            </p>
            <span class="val">${{ personDivision === "" ? "0.00" : personDivision }}</span>
        </div>

        <a v-if="resetButton" href="#" class="btn btn-reset" @click="resetValues">RESET</a>
        <a v-else href="#" class="btn btn-reset off">RESET</a>
    </div>
  </div>
</template>

<script>
export default {
    data() {
      return {
        customTip: "",
        billValue: "",
        people: 0,
        resetButton: false,
        resultTip: "",
        valueTip: "",
        personDivision: "",
      }
    },

    methods: {
      getValue(e) {
        if (this.billValue != '') {
          let target = e.target.innerText.replace("%", "");
          this.valueTip = target;
          this.calcTip()
        } else {
          this.alertEl(".bill")
        }
      },

      calcTip() {

        if (this.people) {
          this.resultTip = Number(((this.billValue * this.valueTip) / 100) + this.billValue).toFixed(2);
          this.personDivision = (this.resultTip / this.people).toFixed(2);

          // Clear input
          this.billValue = "";
          this.resetButton = !this.resetButton;
        } else {
          this.alertEl(".bill");
        }
      },

      calCustom() {
        if (this.people) {
          setTimeout(() => {
            this.resultTip = Number(((this.billValue * this.customTip) / 100) + this.billValue).toFixed(2);
            this.personDivision = (this.resultTip / this.people).toFixed(2)
          }, 1500)
        } else {
          this.alertEl(".number-people")
        }
      },

      resetValues() {
        this.resultTip = "";
        this.personDivision = "";
        this.resetButton = !this.resetButton;
      },

      alertEl(el) {
        let html = `<p class="alert alert-danger">Write some value below</p>`

        document.querySelector(el).insertAdjacentHTML("afterend", html);

        setTimeout(() => {
          document.querySelector(".alert").remove()
        }, 2000)
      }
    }
};
</script>

<style>
.calculator {
  background-color: var(--clr-white);
  max-width: 900px;
  padding: 1em 2em;
  border-radius: 10px;
  font-size: 20px;
}

.btn-tips {
  background-color: var(--clr-very-dark-cyan);
  color: var(--clr-white);
  width: 100px;
  font-weight: bold;
}

.right-side {
  background-color: var(--clr-very-dark-cyan);
  border-radius: 10px;
  max-width: 350px;
  position: relative;
}

.tip {
    font-size: 16px;
    color: var(--clr-white);
}

.tip > .person {
    color: var(--clr-light-grayish-cyan);
    font-size: 12px;
}

.val {
    color: var(--clr-white);
    font-size: 34px;
}

.btn-reset {
    width: 100%;
    margin-top: 7em;
    background-color: var(--clr-strong-cyan);
    font-weight: bold;
    color: var(--clr-white);
}

.off {
  background-color: var(--clr-dark-grayish-cyan);
  color: var(--clr-white);
  pointer-events: none;
  cursor: default;
}

.alert {
  font-size: 12px;
  padding: 8px;
}
</style>