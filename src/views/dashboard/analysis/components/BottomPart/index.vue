<template>
  <n-grid :x-gap="16" :y-gap="16" :item-responsive="true">
    <n-grid-item span="0:24 640:24 1024:8">
      <n-card title="时间线" :bordered="false" class="rounded-16px shadow-sm">
        <div class="h-360px">
          <n-timeline>
            <n-timeline-item v-for="item in timelines" :key="item.type" v-bind="item" />
          </n-timeline>
        </div>
      </n-card>
    </n-grid-item>
    <n-grid-item span="0:24 640:24 1024:16">
      <n-card title="表格" :bordered="false" class="rounded-16px shadow-sm">
        <div class="h-360px">
          <n-data-table size="small" :columns="columns" :data="tableData" />
        </div>
      </n-card>
    </n-grid-item>
    <n-grid-item span="24">
      <n-card title="评级" :bordered="false" class="rounded-16px shadow-sm">
        <div class="h-100%">
          <n-data-table size="small" :columns="scoreColumns" :data="scoresDataCon" :max-height="500" />
        </div>
      </n-card>
    </n-grid-item>
  </n-grid>
</template>

<script setup lang="ts">
import { h } from 'vue';
import { NTag, NRate } from 'naive-ui';

defineOptions({
  name: 'DashboardAnalysisBottomPart',
  mounted() {
    this.init();
  }
});

interface TimelineData {
  type: 'default' | 'info' | 'success' | 'warning' | 'error';
  title: string;
  content: string;
  time: string;
}

interface TableData {
  key: number;
  name: string;
  age: number;
  address: string;
  tags: string[];
}

interface ScoresData {
  id: number;
  name: string;
  score: number;
  rate: number;
}

const timelines: TimelineData[] = [
  { type: 'default', title: '啊', content: '', time: '2021-10-10 20:46' },
  { type: 'success', title: '成功', content: '哪里成功', time: '2021-10-10 20:46' },
  { type: 'error', title: '错误', content: '哪里错误', time: '2021-10-10 20:46' },
  { type: 'warning', title: '警告', content: '哪里警告', time: '2021-10-10 20:46' },
  { type: 'info', title: '信息', content: '是的', time: '2021-10-10 20:46' }
];
const starInfo = {
  '20': 5,
  '40': 4,
  '60': 3,
  '80': 2,
  '100': 1
};
const columns = [
  {
    title: 'Name',
    key: 'name'
  },
  {
    title: 'Age',
    key: 'age'
  },
  {
    title: 'Address',
    key: 'address'
  },
  {
    title: 'Tags',
    key: 'tags',
    render(row: TableData) {
      console.log('row.tags:', row.tags);
      const tags = row.tags.map(tagKey => {
        return h(
          NTag,
          {
            style: {
              marginRight: '6px'
            },
            type: 'info'
          },
          {
            default: () => tagKey
          }
        );
      });
      console.log('abs:', tags);
      return tags;
    }
  }
];

const scoreColumns = [
  {
    title: 'Id',
    key: 'id',
    sorter: 'default',
    defaultSortOrder: 'ascend'
  },
  {
    title: 'Name',
    key: 'name',
    sorter: 'default'
  },
  {
    title: 'Score',
    key: 'score',
    sorter: (row1, row2) => row1.score - row2.score
  },
  {
    title: 'Rate',
    key: 'rate',
    sorter: 'default'
  },
  {
    title: 'Star',
    key: 'star',
    render(row: ScoresData) {
      const tags = [row.rate].map(im => {
        return h(NRate, { size: 'small', readonly: true, count: 5, 'default-value': starInfo[im] });
      });
      // console.log('abs:', tags);
      return tags;
      // return h(
      //   'NTag',
      //   {
      //     style: {
      //       marginRight: '6px',
      //       color: 'red'
      //     },
      //     type: 'primary'
      //   },
      //   {
      //     default: () => starInfo[row.rate]
      //   }
      // );
      // return h('div');
    }
    // render(row: ScoresData) {
    //   // return h('NRate');
    //   return h(
    //     'NRate',
    //     { size: 'small', count: 5, 'default-value': starInfo[row.rate] }
    //     // {
    //     //   default: () =>
    //     // }
    //   );
    // }
  }
];

const tableData: TableData[] = [
  {
    key: 0,
    name: 'John Brown',
    age: 32,
    address: 'New York No. 1 Lake Park',
    tags: ['nice', 'developer']
  },
  {
    key: 1,
    name: 'Jim Green',
    age: 42,
    address: 'London No. 1 Lake Park',
    tags: ['wow']
  },
  {
    key: 2,
    name: 'Joe Black',
    age: 32,
    address: 'Sidney No. 1 Lake Park',
    tags: ['cool', 'teacher']
  },
  {
    key: 3,
    name: 'Soybean',
    age: 25,
    address: 'China Shenzhen',
    tags: ['handsome', 'programmer']
  },
  {
    key: 4,
    name: 'John Brown',
    age: 32,
    address: 'New York No. 1 Lake Park',
    tags: ['nice', 'developer']
  },
  {
    key: 5,
    name: 'Jim Green',
    age: 42,
    address: 'London No. 1 Lake Park',
    tags: ['wow']
  },
  {
    key: 6,
    name: 'Joe Black',
    age: 32,
    address: 'Sidney No. 1 Lake Park',
    tags: ['cool', 'teacher']
  }
];

const scoresData: ScoresData[] = [
  {
    id: 41,
    score: 323633994.23,
    name: 'Campbell',
    rate: 0
  },
  {
    id: 40,
    score: 206316671.32,
    name: 'Camilla',
    rate: 0
  },
  {
    id: 49,
    score: 181000000,
    name: 'Daine',
    rate: 0
  },
  {
    id: 2,
    score: 125000000,
    name: 'Absolon',
    rate: 0
  },
  {
    id: 1,
    score: 100000000,
    name: 'Absalom',
    rate: 0
  },
  {
    id: 43,
    score: 99972583.18,
    name: 'Candida',
    rate: 0
  },
  {
    id: 79,
    score: 70000000,
    name: 'Fairy',
    rate: 0
  },
  {
    id: 54,
    score: 50000000,
    name: 'Dalton',
    rate: 0
  },
  {
    id: 19,
    score: 49089409.6,
    name: 'Babbage',
    rate: 0
  },
  {
    id: 82,
    score: 36000000,
    name: 'Fannie',
    rate: 0
  },
  {
    id: 6,
    score: 31189862.88,
    name: 'Achilles',
    rate: 0
  },
  {
    id: 68,
    score: 30998434.25,
    name: 'Eda',
    rate: 0
  },
  {
    id: 84,
    score: 30000000,
    name: 'Farley',
    rate: 0
  },
  {
    id: 85,
    score: 29000000,
    name: 'Farmer',
    rate: 0
  },
  {
    id: 48,
    score: 25000000,
    name: 'Dailey',
    rate: 0
  },
  {
    id: 47,
    score: 22000000,
    name: 'Dahlia',
    rate: 0
  },
  {
    id: 53,
    score: 20000000,
    name: 'Dallas',
    rate: 0
  },
  {
    id: 83,
    score: 18000000,
    name: 'Fanny',
    rate: 0
  },
  {
    id: 87,
    score: 16000000,
    name: 'Farrah',
    rate: 0
  },
  {
    id: 46,
    score: 14000000,
    name: 'Dahl',
    rate: 0
  },
  {
    id: 81,
    score: 13000000,
    name: 'Fallon',
    rate: 0
  },
  {
    id: 88,
    score: 12000000,
    name: 'Farrar',
    rate: 0
  },
  {
    id: 86,
    score: 11500000,
    name: 'Farr',
    rate: 0
  },
  {
    id: 50,
    score: 10000000,
    name: 'Daisy',
    rate: 0
  },
  {
    id: 65,
    score: 9891004.88,
    name: 'Eastman',
    rate: 0
  },
  {
    id: 18,
    score: 9493220.55,
    name: 'Babb',
    rate: 0
  },
  {
    id: 80,
    score: 8000000,
    name: 'Faith',
    rate: 0
  },
  {
    id: 77,
    score: 6000000,
    name: 'Fair',
    rate: 0
  },
  {
    id: 92,
    score: 5929589.04,
    name: 'Gage',
    rate: 0
  },
  {
    id: 25,
    score: 5000000,
    name: 'Babette',
    rate: 0
  },
  {
    id: 89,
    score: 2833044.36,
    name: 'Farrell',
    rate: 0
  },
  {
    id: 70,
    score: 2591937.85,
    name: 'Eddy',
    rate: 0
  },
  {
    id: 42,
    score: 2509182.45,
    name: 'Candace',
    rate: 0
  },
  {
    id: 22,
    score: 1823393.68,
    name: 'Babbs',
    rate: 0
  },
  {
    id: 33,
    score: 1540008.49,
    name: 'Caldwell',
    rate: 0
  },
  {
    id: 32,
    score: 1486959.2,
    name: 'Calderon',
    rate: 0
  },
  {
    id: 10,
    score: 845886.22,
    name: 'Ackroyd',
    rate: 0
  },
  {
    id: 37,
    score: 775634.05,
    name: 'Calvert',
    rate: 0
  },
  {
    id: 31,
    score: 769712.11,
    name: 'Cain',
    rate: 0
  },
  {
    id: 30,
    score: 751955.81,
    name: 'Cahill',
    rate: 0
  },
  {
    id: 21,
    score: 733665.7,
    name: 'Babbitt',
    rate: 0
  },
  {
    id: 36,
    score: 671439.88,
    name: 'Calloway',
    rate: 0
  },
  {
    id: 29,
    score: 619793.78,
    name: 'Bacchus',
    rate: 0
  },
  {
    id: 78,
    score: 220312.77,
    name: 'Fairchild',
    rate: 0
  },
  {
    id: 44,
    score: 204571.5,
    name: 'Cannon',
    rate: 0
  },
  {
    id: 74,
    score: 201093.09,
    name: 'Edison',
    rate: 0
  },
  {
    id: 28,
    score: 145836.61,
    name: 'Babur',
    rate: 0
  },
  {
    id: 90,
    score: 142261.37,
    name: 'Gabriel',
    rate: 0
  },
  {
    id: 8,
    score: 132723.36,
    name: 'Ackers',
    rate: 0
  },
  {
    id: 73,
    score: 110180.76,
    name: 'Edie',
    rate: 0
  },
  {
    id: 3,
    score: 81496.8,
    name: 'Achard',
    rate: 0
  },
  {
    id: 4,
    score: 81496.8,
    name: 'Achebe',
    rate: 0
  },
  {
    id: 75,
    score: 58706.77,
    name: 'Fabian',
    rate: 0
  },
  {
    id: 23,
    score: 22284.95,
    name: 'Babcock',
    rate: 0
  },
  {
    id: 69,
    score: 12750.23,
    name: 'Eddie',
    rate: 0
  },
  {
    id: 45,
    score: 10037.52,
    name: 'Dagmar',
    rate: 0
  },
  {
    id: 38,
    score: 7542.74,
    name: 'Calvin',
    rate: 0
  },
  {
    id: 35,
    score: 5572.37,
    name: 'Callie',
    rate: 0
  },
  {
    id: 71,
    score: 4640.18,
    name: 'Eden',
    rate: 0
  },
  {
    id: 11,
    score: 4335.04,
    name: 'Acland',
    rate: 0
  },
  {
    id: 13,
    score: 4335.04,
    name: 'Acuff',
    rate: 0
  },
  {
    id: 27,
    score: 1387.28,
    name: 'Babs',
    rate: 0
  },
  {
    id: 64,
    score: 465.68,
    name: 'Easter',
    rate: 0
  },
  {
    id: 61,
    score: 425.15,
    name: 'Earle',
    rate: 0
  },
  {
    id: 16,
    score: 200,
    name: 'Baal',
    rate: 0
  },
  {
    id: 20,
    score: 200,
    name: 'Babbie',
    rate: 0
  },
  {
    id: 66,
    score: 197.82,
    name: 'Eaton',
    rate: 0
  },
  {
    id: 56,
    score: 166.31,
    name: 'Damaris',
    rate: 0
  },
  {
    id: 72,
    score: 137.19,
    name: 'Edgar',
    rate: 0
  },
  {
    id: 60,
    score: 132.72,
    name: 'Earl',
    rate: 0
  },
  {
    id: 26,
    score: 74.11,
    name: 'Babington',
    rate: 0
  },
  {
    id: 24,
    score: 59.79,
    name: 'Baber',
    rate: 0
  },
  {
    id: 91,
    score: 46.13,
    name: 'Gabrielle',
    rate: 0
  },
  {
    id: 76,
    score: 28.62,
    name: 'Fagan',
    rate: 0
  },
  {
    id: 14,
    score: 27.24,
    name: 'Adah',
    rate: 0
  },
  {
    id: 12,
    score: 21.15,
    name: 'Acton',
    rate: 0
  },
  {
    id: 39,
    score: 21.06,
    name: 'Cameron',
    rate: 0
  },
  {
    id: 57,
    score: 17.78,
    name: 'Damian',
    rate: 0
  },
  {
    id: 63,
    score: 16.76,
    name: 'Eason',
    rate: 0
  },
  {
    id: 9,
    score: 15,
    name: 'Ackland',
    rate: 0
  },
  {
    id: 5,
    score: 10,
    name: 'Acheson',
    rate: 0
  },
  {
    id: 51,
    score: 9.81,
    name: 'Dale',
    rate: 0
  },
  {
    id: 55,
    score: 9.55,
    name: 'Daly',
    rate: 0
  },
  {
    id: 17,
    score: 5,
    name: 'Bab',
    rate: 0
  },
  {
    id: 62,
    score: 3.96,
    name: 'Early',
    rate: 0
  },
  {
    id: 67,
    score: 3.34,
    name: 'Ed',
    rate: 0
  },
  {
    id: 15,
    score: 2.73,
    name: 'Baade',
    rate: 0
  },
  {
    id: 59,
    score: 1.9,
    name: 'Dan',
    rate: 0
  },
  {
    id: 58,
    score: 1.44,
    name: 'Damon',
    rate: 0
  },
  {
    id: 52,
    score: 0.84,
    name: 'Daley',
    rate: 0
  },
  {
    id: 34,
    score: 0.74,
    name: 'Caleb',
    rate: 0
  },
  {
    id: 7,
    score: 0.36,
    name: 'Acker',
    rate: 0
  }
];

const scoresDataCon: ScoresData[] = [];

function init(): void {
  const uniScoresSorted = [...new Set(this.scoresData)].sort((a, b) => b.score - a.score);
  const ratio = 0.2;
  const uniScoresLenth = uniScoresSorted.length;
  const rangeNum = Math.ceil(1 / ratio);

  console.log('page init...', uniScoresSorted, uniScoresLenth, rangeNum);
  // console.log('page init...');
  const rangeArr = [];
  for (let i = 0; i < rangeNum; i++) {
    rangeArr.push(Math.round(uniScoresLenth * ratio * (i + 1)));
  }
  console.log('根据比例去划分区间段', rangeArr);
  for (const im of this.scoresData) {
    console.log(im);
    for (const ind in rangeArr) {
      console.log(ind);
      if (im.score >= uniScoresSorted[rangeArr[ind] - 1].score) {
        im.rate = (ind * 1 + 1) * (ratio * 100);
        break;
      }
    }
  }
  console.log('this.scoresData:', this.scoresData);
  this.scoresDataCon = this.scoresData;
  // this.scoresData = [];
  // for (const n of 'asd') {
  //   console.log(n);
  // }
}
</script>

<style scoped></style>
