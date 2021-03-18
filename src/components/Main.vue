<template>
  <div class="container">
    <div class="info" v-show="info.length">
      <ul v-for="(file, key) of info" :key="key">
        <li>Тип: {{ file.type }}</li>
        <li>Имя: {{ file.name }}</li>
        <li>Количество скачиваний: {{ file.hits }}</li>
      </ul>
      <button class="btn btn-dark" @click="hideInfo">Закрыть</button>
    </div>
    <div>
      <div class="search row justify-content-between">
        <label>
          Поиск
          <input v-model.trim="search" v-on:keyup="filtered" type="text">
        </label>
        <div class="paginator d-flex justify-content-between">
          <button class="btn btn-danger" :disabled="start === 0" @click="pagination('back')">Назад</button>
          <button class="btn btn-danger" :disabled="end === lists.length" @click="pagination('forward')">Вперед</button>
        </div>
      </div>
      <div>
        <table class="table table-bordered table-hover">
          <thead>
          <tr>
            <th>Type</th>
            <th>Name</th>
          </tr>
          </thead>
          <tbody v-for="(item, key) in lists.slice(start, end)" :key="key">
          <tr @click="showInfo(item.name)">
            <td>{{ item.type }}</td>
            <td>{{ item.name }}</td>
          </tr>
          </tbody>
        </table>
      </div>
    </div>

  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: "Main",
  data() {
    return {
      data: [],
      lists: [],
      info: [],
      search: '',
      step: 10,
      start: 0,
      end: 10,
    }
  },
  methods: {
    getData() {
      axios.get("https://data.jsdelivr.com/v1/stats/packages/year").then(res => this.lists = res.data);
    },
    pagination(arrow) {
      if (arrow === "back") {
        if (this.start > 0) {
          this.start -= this.step;
          this.end -= this.step;
        }
      } else {
        if (this.end < this.lists.length) {
          this.start += this.step;
          this.end += this.step;
        }
      }
    },
    showInfo(name) {
      this.info = this.lists.filter(item => item.name === name);
    },
    hideInfo() {
      this.info = [];
    },
    filtered() {

      axios.get("https://data.jsdelivr.com/v1/stats/packages/year").then(res => this.data = res.data);
      this.lists = this.data.filter(str => str.name.toLowerCase().indexOf(this.search.toLowerCase()) + 1);
      if (!this.search) {
        axios.get("https://data.jsdelivr.com/v1/stats/packages/year").then(res => this.lists = res.data);
      }
    }
  },
  mounted() {
    this.getData();
  }

}
</script>

<style scoped lang="scss">
.container {
  flex: auto;
}

.info {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #161931;
  padding: 20px;
  border-radius: 24px;
  z-index: 9;
  ul {
    list-style: none;
    color: #fff;
  }
  .btn {
    display: block;
    margin: 0 auto;
  }
}

input {
  width: 100%;
  border-radius: 8px;
}

.paginator {
  width: 25%;
  margin-top: 20px;
}

table {
  width: 40%;
  max-height: 50vh;
  margin: 0 auto;
  overflow: auto;
}

th {
  color: goldenrod;
  text-align: center;
  border: 1px solid gray;
  font-size: 24px;
}

td {
  padding: 5px 10px;
  color: #ffffff;
  position: relative;
  border: 1px solid gray;
  cursor: pointer;

  &:nth-child(1) {
    width: 25%;
  }
}
</style>
