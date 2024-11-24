var co2_threshold = 600; // Пороговое значение CO2
var vok_threshold = 400;  // Пороговое значение VOC
var blink_interval = 500; // Интервал мигания в миллисекундах

var co2_blinking = false; // Флаг мигания зелёного светодиода
var vok_blinking = false; // Флаг мигания красного светодиода

function startBlinkingGreen() {
  if (dev["wb-msw-v4_1_2"]["CO2"] > co2_threshold) {
    dev["wb-msw-v4_1_2"]["Green LED"] = !dev["wb-msw-v4_1_2"]["Green LED"];
    setTimeout(startBlinkingGreen, blink_interval);
  } else {
    dev["wb-msw-v4_1_2"]["Green LED"] = false;
    co2_blinking = false;
  }
}

function startBlinkingRed() {
  if (dev["wb-msw-v4_1_2"]["Air Quality (VOC)"] > vok_threshold) {
    dev["wb-msw-v4_1_2"]["Red LED"] = !dev["wb-msw-v4_1_2"]["Red LED"];
    setTimeout(startBlinkingRed, blink_interval);
  } else {
    dev["wb-msw-v4_1_2"]["Red LED"] = false;
    vok_blinking = false;
  }
}

defineRule("check_CO2_and_VOC", {
  whenChanged: ["wb-msw-v4_1_2/CO2", "wb-msw-v4_1_2/Air Quality (VOC)"],
  then: function () {
    checkThresholds();
  }
});

function checkThresholds() {
  if (dev["wb-msw-v4_1_2"]["CO2"] > co2_threshold && !co2_blinking) {
    co2_blinking = true;
    startBlinkingGreen();
  }

  if (dev["wb-msw-v4_1_2"]["Air Quality (VOC)"] > vok_threshold && !vok_blinking) {
    vok_blinking = true;
    startBlinkingRed();
  }
}
