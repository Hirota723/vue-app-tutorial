<template>
  <div class="container">
    <div class="clock">
      <div class="date">
        <p>{{ year }}/{{ month }}/{{ day }}</p>
      </div>
      <div class="time">
        <p>
          {{ hour }}:{{ minute }}<span class="seconds">:{{ second }}</span>
        </p>
      </div>
      <div class="button" v-on:click="showMessage()">
        <p>10秒後にアラームを設定</p>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  name: "ClockScreen",
  data() {
    return {
      // 現在の日時を保持
      date: new Date(),
    };
  },
  computed: {
    // 年
    year() {
      return this.date.getFullYear();
    },
    // 月
    month() {
      return this.date.getMonth() + 1;
    },
    // 日
    day() {
      return this.dateTimePadding(this.date.getDate());
    },
    // 時
    hour() {
      return this.dateTimePadding(this.date.getHours());
    },
    // 分
    minute() {
      return this.dateTimePadding(this.date.getMinutes());
    },
    // 秒
    second() {
      return this.dateTimePadding(this.date.getSeconds());
    },
  },
  mounted() {
    // 現在日時をセット
    this.setDate();
    // 1秒ごとに現在日時を更新
    setInterval(() => {
      this.setDate();
    }, 1000);
  },
  methods: {
    // 日時を2桁に変換
    dateTimePadding(num: number) {
      return ("0" + num).slice(-2);
    },

    // 現在日時をセット
    setDate() {
      this.date = new Date();
    },

    // 10秒後にアラームを設定
    showMessage() {
      setTimeout(() => {
        alert("10秒経過しました！");
      }, 10000);
    },
  },
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.container {
  display: flex;
  flex-flow: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #262626;
}

.date,
.time {
  font-weight: bold;
  color: #00ff01;
}

.date {
  font-size: 16px;
  text-align: right;
}
.time {
  font-size: 70px;
  padding: 40px 0;
}
.seconds {
  font-size: 30px;
}
.button {
  border: 1px solid white;
  text-align: center;
  padding: 10px 0;
  color: white;
  cursor: pointer;
}
</style>
