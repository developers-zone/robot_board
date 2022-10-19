<script setup>
import $ from "jquery";
import { ref } from "vue";

const player = ref("X");
const board = ref([
  ["", "", "", "", ""],
  ["", "", "", "", ""],
  ["", "", "", "", ""],
  ["", "", "", "", ""],
  ["", "", "", "", ""],
]);
const MoveRobot = (move) => {
  if (move === 0) {
    var robot_board = $(".robot_board").parent("div").html();

    if ($(".robot_board").hasClass("robot-right")) {
      $(".robot_board")
        // .remove()
        .parent("div")
        .next(".robot_parent")
        .append(robot_board);
      $(".robot_board").first().remove();
    } else if ($(".robot_board").hasClass("robot-left")) {
      $(".robot_board")
        // .remove()
        .parent("div")
        .prev(".robot_parent")
        .append(robot_board);
      $(".robot_board").last().remove();
    } else {
      $(".robot_board")
        // .remove()
        .parent("div")
        .next(".robot_parent")
        .append(robot_board);
      $(".robot_board").first().remove();
    }

    // console.log(robot_board);
    // $(".robot_board").parent("div").next(".robot_parent").append(robot_board);
    // .remove()
    console.log(move, "straight");
  } else if (move === 1 && !$(".robot_board").hasClass("robot-left")) {
    if ($(".robot_board").hasClass("robot-right")) {
      $(".robot_board").removeClass("robot-right");
    }
    $(".robot_board").addClass("robot-left");
    console.log(move, "left");
  } else if (move === 2 && !$(".robot_board").hasClass("robot-right")) {
    if ($(".robot_board").hasClass("robot-left")) {
      $(".robot_board").removeClass("robot-left");
    }
    $(".robot_board").addClass("robot-right");
    console.log(move, "right");
  }

  if ($(".robot_board").parent("div").find(".robot_destiny").length) {
    setTimeout(function () {
      alert("Congratulations.!! Robot has reached the destination.!! ");
      location.reload();
    }, 500);
  }
};
</script>

<template>
  <main class="pt-8 text-center">
    <h1 class="mb-8 text-3xl font-bold uppercase">Robot LeaderBoard</h1>

    <span class="gameboard scoreboard">Score: 6</span>
    <span class="gameboard timespan">Time: 32</span>
    <div class="flex flex-col items-center mb-8">
      <div v-for="(row, x) in board" :key="x" class="flex">
        <div
          v-for="(cell, y) in row"
          :key="y"
          :class="`robot_parent border border-black w-24 h-24 flex items-center justify-center material-icons-outlined text-4xl cursor-pointer ${
            cell === 'X' ? 'text-pink-500' : 'text-blue-400'
          }`"
        >
          <span
            class="material-symbols-outlined robot_board"
            v-if="x === 2 && y === 2"
          >
            smart_toy
          </span>

          <span
            class="material-symbols-outlined robot_destiny"
            v-if="x === 2 && y === 4"
          >
            star
          </span>
        </div>
      </div>
    </div>

    <div class="material-icons-outlined text-center text-5xl">
      <button @click="MoveRobot(1)" title="Turn 90 degree leftwards">
        <span class="material-symbols-outlined"> turn_left </span>
      </button>
      <button @click="MoveRobot(0)" title="Move straight">
        <span class="material-symbols-outlined"> straight </span>
      </button>
      <button @click="MoveRobot(2)" title="Turn 90 degree rightwards">
        <span class="material-symbols-outlined"> turn_right </span>
      </button>
    </div>
  </main>
</template>

<style scoped>
.robot-left {
  transform: rotate(-90deg);
}
.robot-right {
  transform: rotate(90deg);
}
.gameboard {
  font-weight: bold;
  margin-top: -6%;
}
.gameboard.scoreboard {
  float: left;
}
.gameboard.timespan {
  float: right;
}
</style>
