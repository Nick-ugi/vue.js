<template>
  <div>
    <p v-bind:title="msg">{{ msg }}</p>
    <p v-if="testIf == '1'">if == 1</p>
    <p v-else-if="testIf == '2'">else if == 2</p>
    <p v-else>else == ?</p>
    <input type="number" v-model.number="testIf">
    <button v-on:click="addBtn">더하기버튼</button>
  </div>
  <div>
    <basicGrid v-bind:gridData="gridData"/>
    이름 : <input type="text" v-model="testName">-
    번호 : <input type="text" v-model="testNum">-
    나이 : <input type="text" v-model="testAge">
    <button v-on:click="addData">데이터 추가</button>
    <button v-on:click="axiosData">axios데이터 추가</button>
  </div>
</template>

<script>
import basicGrid from '@/components/basicGrid.vue';
import axios from 'axios'
export default {
  name: 'VueHello',
  data() {
    return {
      msg: 'vue hello~',
      testIf: '',
      gridData : {
        header : ['이름', '번호', '나이'],
        rows : [
          {'이름' : '신동환','번호':'1','나이':'30'},
          {'이름' : '김동욱','번호':'2','나이':'29'},
          {'이름' : '김홍석','번호':'3','나이':'30'}
        ]
      },
      //변수 초기화,
        testName:'',
        testNum:'',
        testAge:''
    };
  },

  methods: {
    addBtn() {
      this.testIf++
    }
  },
  methods: {
    addData() {
      this.gridData.rows.push({
        '이름': this.testName,
        '번호': this.testNum,
        '나이': this.testAge
      })
  },
  axiosData() {
  axios
    .get('https://jsonplaceholder.typicode.com/todos')
    .then(res => {
      console.log(res.data);
      if (res.data.length > 0) {
        var keys = []
        for (let i = 0; i < res.data.length; i++) {
          const key = res.data[i];
          keys.push({  // keys에 데이터 삽입, keys 에는, key.data(변수명에 맞는 데이터)가 들어감

            'userId': key.userId,
            'id': key.id,
            'title': key.title,
            'completed': key.completed
          });
        }
        // 헤더 설정
        this.gridData.header = ['userId', 'id', 'title', 'completed'];
        // rows 설정
        this.gridData.rows = keys;
      }
    })
    .catch(error => {
      console.error('Error fetching data:', error);
    });
}
  },
  components : {basicGrid}
}
</script>