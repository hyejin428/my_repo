/* eslint-disable vue/no-parsing-error */
/* eslint-disable vue/no-parsing-error */
<template>
  <div class = "Hello">
    <v-container row wrap id="scroll-target" class="scroll-y">
      <v-flex lg6>

        <v-layout column class="pa-10" v-scroll:#scroll-target="onScroll">
          <h3 class="display-1 pa-3">
              뉴스 주제
          </h3>

          <v-bottom-navigation
            :value="activeBtn"
            color="blue"
            grow
            flat
          >
            <v-btn class="title">주제1</v-btn>
            <v-btn class="title">주제2</v-btn>
            <v-btn class="title">주제3</v-btn>
            <v-btn class="title">주제4</v-btn>

          </v-bottom-navigation>

          <h3 class="display-1 pa-3">
              기사 모음
          </h3>
          <v-card>
            <v-tabs
              v-model="tab"
              background-color="primary"
              dark
            >
              <v-tab
                v-for="item in items_title"
                :key="item.tab"
              >
                {{ item.tab }}
              </v-tab>
            </v-tabs>
            <v-container
              id="scroll-target"
              style="max-height: 400px"
              class="overflow-y-auto"
            >
              <v-tabs-items v-model="tab"
                v-scroll:#scroll-target="onScroll"
                style="height: 1000px">
                <v-tab-item
                  v-for="(item, i) in lineTest"
                    :key="i"
                >
                  <v-card flat>
                    <v-card-text v-html="item.content"></v-card-text>
                  </v-card>
                </v-tab-item>
              </v-tabs-items>
            </v-container>
          </v-card>

			<h3 class="display-1 pa-3">
				댓글 모음
			</h3>

			<v-card>
				<v-tabs
				v-model="tab2"
				background-color="primary"
				dark
				>
          <v-tab>좋아요 순</v-tab>
          <v-tab>댓글 순</v-tab>
          <v-tab>공감비율 순</v-tab>
          <v-tab>감정 순</v-tab>

				</v-tabs>

				<v-container
				id="scroll-target"
				style="max-height: 400px"
				class="overflow-y-auto"
				>
				<v-tabs-items v-model="tab2"
					v-scroll:#scroll-target="onScroll"
					style="height: 1000px">
          <!-- 좋아요순 -->
					<v-tab-item>
						<v-card flat>
						<v-list dense shaped>
							<!-- <template v-for="(item,idx) in item1.reply"> -->
              <template v-for="(item) in like_order_list">
								<v-list-item
								:key="item['naver_news_id']"
								v-on:click="greet"
								>
                 <v-list-item-avatar>
                  <v-icon>mdi-emoticon</v-icon>
                </v-list-item-avatar>
								<v-list-item-content>
									<v-list-item-title v-text="item['reply']"></v-list-item-title>
									<v-list-item-subtitle v-text="item['date_time']"></v-list-item-subtitle>
								</v-list-item-content>

								<div>
									<v-btn class="ma-2" text icon color="blue lighten-2">
										<v-icon>mdi-thumb-up</v-icon>
									</v-btn>
									{{item['like_num']}}
									<v-btn class="ma-2" text icon color="red lighten-2">
										<v-icon>mdi-thumb-down</v-icon>
									</v-btn>
									{{item['hate_num']}}
								</div>
								</v-list-item>
							</template>
						</v-list>
						</v-card>
					</v-tab-item>
          <!-- 댓글순 -->
          <v-tab-item>
						<v-card flat>
						<v-list dense shaped>
							<!-- <template v-for="(item,idx) in item1.reply"> -->
              <template v-for="(item) in reply_order_list">
								<v-list-item
								:key="item['naver_news_id']"
								v-on:click="greet"
								>
                 <v-list-item-avatar>
                  <v-icon>mdi-emoticon</v-icon>
                </v-list-item-avatar>
								<v-list-item-content>
									<v-list-item-title v-text="item['reply']"></v-list-item-title>
									<v-list-item-subtitle v-text="item['date_time']"></v-list-item-subtitle>
								</v-list-item-content>

								<div>
									<v-btn class="ma-2" text icon color="blue lighten-2">
										<v-icon>mdi-thumb-up</v-icon>
									</v-btn>
									{{item['like_num']}}
									<v-btn class="ma-2" text icon color="red lighten-2">
										<v-icon>mdi-thumb-down</v-icon>
									</v-btn>
									{{item['hate_num']}}
								</div>
								</v-list-item>
							</template>
						</v-list>
						</v-card>
					</v-tab-item>
          <!-- 공감비율순 -->
          <v-tab-item>
						<v-card flat>
						<v-list dense shaped>
							<!-- <template v-for="(item,idx) in item1.reply"> -->
              <template v-for="(item) in like_rate_order_list">
								<v-list-item
								:key="item['naver_news_id']"
								v-on:click="greet"
								>
                 <v-list-item-avatar>
                  <v-icon>mdi-emoticon</v-icon>
                </v-list-item-avatar>
								<v-list-item-content>
									<v-list-item-title v-text="item['reply']"></v-list-item-title>
									<v-list-item-subtitle v-text="item['date_time']"></v-list-item-subtitle>
								</v-list-item-content>

								<div>
									<v-btn class="ma-2" text icon color="blue lighten-2">
										<v-icon>mdi-thumb-up</v-icon>
									</v-btn>
									{{item['like_num']}}
									<v-btn class="ma-2" text icon color="red lighten-2">
										<v-icon>mdi-thumb-down</v-icon>
									</v-btn>
									{{item['hate_num']}}
								</div>
								</v-list-item>
							</template>
						</v-list>
						</v-card>
					</v-tab-item>
          <!-- 감정순 -->
          <v-tab-item>
						<v-card flat>
						<v-list dense shaped>
							<!-- <template v-for="(item,idx) in item1.reply"> -->
              <template v-for="(item) in sent_order_list">
								<v-list-item
								:key="item['naver_news_id']"
								v-on:click="greet"
								>
                 <v-list-item-avatar>
                  <v-icon>mdi-emoticon</v-icon>
                </v-list-item-avatar>
								<v-list-item-content>
									<v-list-item-title v-text="item['reply']"></v-list-item-title>
									<v-list-item-subtitle v-text="item['date_time']"></v-list-item-subtitle>
								</v-list-item-content>

								<div>
									<v-btn class="ma-2" text icon color="blue lighten-2">
										<v-icon>mdi-thumb-up</v-icon>
									</v-btn>
									{{item['like_num']}}
									<v-btn class="ma-2" text icon color="red lighten-2">
										<v-icon>mdi-thumb-down</v-icon>
									</v-btn>
									{{item['hate_num']}}
								</div>
								</v-list-item>
							</template>
						</v-list>
						</v-card>
					</v-tab-item>
				</v-tabs-items>
				</v-container>
			</v-card>

			<GChart id="gg"
				type="ScatterChart"
				:data="chartData"
				:options="chartOptions"
				:events="chartEvents"
				ref="gChart"
			/>

      <!-- <v-card
        class="mx-auto"
        max-width="300"
        tile
      >
        <v-list disabled>
          <v-list-item-group v-model="test_item" color="primary">
            <v-list-item
              v-for="(item, i) in db_replies"
              :key="i"
            >
              <v-list-item-content>
                <v-list-item-title v-text="item.nickname"></v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list-item-group>
        </v-list>
      </v-card> -->
      <!-- <p>{{ like_order_list }}</p> -->

        </v-layout>
      </v-flex>

      <v-flex lg6>
        <v-layout column class="pa-10">
          <!-- <h3 class="display-1 pa-3">
              Veracity Check
          </h3> -->
          <!-- <v-flex row>
            <v-text-field
              label="Outlined"
              single-line
              outlined
              placeholder="기사 본문의 문장을 입력해주세요"
            ></v-text-field>
            <v-btn color="primary" dark x-large class="pa-3">Check</v-btn>
          </v-flex> -->
          <!-- <v-flex row>
            <h3 class="body-1 pa-3">
                결과:
            </h3>
            <v-card>
              <h3 class="body-1 pa-3">
                  40%
              </h3>
            </v-card>
          </v-flex> -->

          <h3 class="display-1 pa-3 mt-5">
              지식 그래프 시각화
          </h3>
          <v-flex row>
            <v-text-field
              label="Outlined"
              single-line
              outlined
              placeholder="검색을 원하는 단어를 입력해주세요"
            ></v-text-field>
            <v-btn color="primary" dark x-large class="pa-3">Check</v-btn>
          </v-flex>
          <label> Node size  </label>
          <input type="range" min="1" max="100" v-model='nodeSize' /> {{ options.nodeSize }}
          <label> force </label>
          <input type="range" min="100" max="3000" v-model='force' /> {{ options.force }}

					<!-- KNOWLEDGE GRAPH -->
          <div id="app">
            <!-- <svg @click="setZoom" class="container" :width="viewer.w" :height="viewer.h" ref="svg">
              <g :transform="`translate(${zoom.x},${zoom.y})scale(${zoom.k})`">
                <d3-network ref='net' :net-nodes="nodes" :net-links="links" :options="options"  :link-cb="lcb"/>
              </g>
               <d3-network ref='net' :net-nodes="nodes" :net-links="links" :options="options"  :link-cb="lcb"/>
            </svg> -->
            <!-- <d3-network ref='net' :net-nodes="nodes" :net-links="links" :options="options"  :link-cb="lcb"/> -->
            <d3-network ref='net' :net-nodes="kgNode" :net-links="links" :options="options"  :link-cb="lcb"/>
          </div>

            
          <h3 class="display-1 pa-3">
              댓글 분석 결과 보기
          </h3>

          <template>
            <v-data-table dense 
            v-model="select"
            :headers="headers"
            :items="data"
            :single-select="singleSelect"
            item-key="nickname"
            class="elevation-1"
          >
            </v-data-table>
          </template>

          <template>
            <v-data-table dense 
            v-model="select"
            :headers="headers2"
            :items="data2"
            :single-select="singleSelect"
            item-key="nickname"
            class="elevation-1"
            light
          >
            </v-data-table>
          </template>

          <div></div>

          <v-card class="mt-10">
            <v-tabs
              v-model="tab4"
              background-color="primary"
              dark
            >
              <v-tab
                v-for="item in items4"
                :key="item.tab"
              >
                {{ item.tab }}
              </v-tab>
            </v-tabs>

            <v-tabs-items v-model="tab4">
              <v-tab-item
                v-for="item in items4"
                :key="item.tab"
              >
                <v-card flat>
                  <v-card-text>{{ item.content }}</v-card-text>
                </v-card>
              </v-tab-item>
            </v-tabs-items>
          </v-card>

        </v-layout>
      </v-flex>

    </v-container>
  </div>
</template>



<script>
import newsjj from '../assets/jj.json'
import lineTest from '../assets/line_test.json'
import naverReply from '../assets/corona_naver_news_reply.json'
import D3Network from 'vue-d3-network'
import * as d3 from 'd3'
import axios from 'axios';
// import curComment from '../assets/cur_comments_info_df.json'
// import userInfo from '../assets/user_info_df.json'
import kgLink from '../assets/kg_link2.json'
import kgNode from '../assets/kg_node2.json'
import kgList from '../assets/kg_list2.json'
import nodeNameList from '../assets/node_name_list2.json'
import cur_comments_info_df from '../assets/cur_comments_info_df.json'
import { GChart } from 'vue-google-charts'
// import VueGoogleCharts from 'vue-google-charts'

export default {
  el: '#app',
  components: {
	D3Network,
	GChart
  },
  name: 'UserList',
  data () {
    // var time_senti = new Array();
    let json = require('../assets/cur_comments_info_df.json');
    var data_table = new Array();
    var date_sent = new Array();
    var col = new Array();
    var col2 = new Array();
    col.push({type:"date",label:"Date",id:"date"})
    col.push({type:"number",label:"sentiment",id:"sentiment"})
    col.push({type:"number",label:"id",id:"id"})
    col2.push({type:"date",label:"Date",id:"date"})
    col2.push({type:"number",label:"sentiment",id:"sentiment"})
    data_table.push(col)
    date_sent.push(col2)
		for(let i=0; i<json.length; i++){
      var arr = new Array();
      var arr2 = new Array();
			var date = new Date(json[i]['date']);
      var sentiment = json[i]['sentiment'];
      var id = json[i]['naver_news_comments_id']
			arr.push(date);
      arr.push(sentiment);
      arr.push(id);
      arr2.push(date);
      arr2.push(sentiment);
      data_table.push(arr);
      date_sent.push(arr2);
    }
    
    // <date_sent>
    // date |  sentiment
    // 2019 |  0.3

    // <data_table>
    // date |  sentiment |  id
    // 2019 |  0.3       |  83
    
    return {
      test_item: 1,
      test_items: [
        { text: 'Real-Time', icon: 'mdi-clock' },
        { text: 'Audience', icon: 'mdi-account' },
        { text: 'Conversions', icon: 'mdi-flag' },
      ],
      viewer: {
          w: 600,
          h: 600
      },
      zoom: {
          x: 20,
          y: 0,
          k: 1
      },
      chartEvents: {
        'select': () => {         
          const table = this.$refs.gChart.chartObject;
          const selection = table.getSelection();
          var row = selection[0].row;
          var reply_id = data_table[row][2]

          // var idx = table.indexOf(selection)
          // var idOfObj = data_table[idx][2]
          var newArr = json.filter(function(item){    
            return item.naver_news_comments_id === reply_id;
          });
          // selection[0].row, selection[0].column
          // var value = table.getValue(0,0)
          const onSelectionMeaasge = selection.length !== 0 ? JSON.stringify(newArr[0]['reply']) : 'row was diselected'
          alert(onSelectionMeaasge);
        }
      },
			chartData: date_sent,
      chartOptions: {
				chart: {
					title: 'Age vs. Weight comparison',
          hAxis: {title: 'date'},
          vAxis: {title: 'sentiment'},
          legend: 'none'
				},
				// colors: ['red','#004411'],
				crosshair: { trigger: 'both' }
      },
      singleSelect: false,
      select: [],
      headers: [
          {
            text: 'Nickname',
            align: 'start',
            sortable: false,
            value: 'nickname',
          },
          { text: 'user_nick', value: 'user_nick' },
          { text: 're_reply_num', value: 're_reply_num' },
          { text: 'like', value: 'like' },
          { text: 'hate', value: 'hate' },
          { text: 'sentiment', value: 'sentiment' },
        ],
      "data": [
        {
          "nickname": "pode****",
          "user_nick": "포대",
          "reply": "공기 감염 되네",
          "date": "2006-04-09",
          "re_reply_num": "17",
          "like": "290",
          "hate": "6",
          "sentiment": "0.21"
        },
        {
          "nickname": "mkba****",
          "user_nick": "자유가 아니면 죽음을",
          "reply": "구로 콜센터-한사무실에 있기만 해도 100명이 감염!.. 에레베타에서 2분간 같이 있었는데 감염!... 공기중 감염이 심히 의심되는 상황!... 우한폐렴은 일찍 인류가 경험한적 없는 중국인민해방군에서 만든 인공바이러스!.. 에볼라의 가공할 전염력과 에이즈의 긴 잠복기를 가진! 인류를 멸망시킬수도있는 대재앙!.. 폐렴뿐만 아니라 면역시스템 붕괴의 전형적인 에이즈 바이러스의 특성을 보인다는 논문도 나왔음!... 중국은 판도라의 상자를 연것임!.. 이제 중국문을 걸어잠그는 수준이 아니라! 악마제국 중국과의 단교를 진지하게 논의해 봐야함!",
          "date": "2006-04-09",
          "re_reply_num": "14",
          "like": "298",
          "hate": "40",
          "sentiment": "0.99"
        },
        {
          "nickname": "5982****",
          "user_nick": "598",
          "reply": "그럼 면 마스크도 괜찮다고 하는 정부의 말은 헛소리였네~~~~ 문재인 정부가 잘못된 정보로 국민들을 사지로 몰아 넣는구나~~~ㅠㅠ",
          "date": "2006-04-09",
          "re_reply_num": "4",
          "like": "302",
          "hate": "91",
          "sentiment": "0.99"
        },
        {
          "nickname": "pkpk****",
          "user_nick": "pkp",
          "reply": "에어로졸까지 된다는데 면마스크 쓰자고 한게 누구더라 ㅋㅋㅋㅋㅋㅋㅋ 심지어 마스크 안써도된다면서? ㅋㅋㅋㅋㅋㅋ 이레놓고 해외에서 우리 칭찬한다고 틈만나면 자화자찬 못해서 근질근질",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "61",
          "hate": "8",
          "sentiment": "0.0"
        },
        {
          "nickname": "hjsh****",
          "user_nick": "샤이니",
          "reply": "구로 콜센타 1층이 중국은행입니다, 입국한지 얼마안된 중국이들이 여기서 환전하고 들락랄락 합니다 이래도 중국인 감염전파 아닙니까?",
          "date": "2006-04-09",
          "re_reply_num": "1",
          "like": "56",
          "hate": "5",
          "sentiment": "0.01"
        },
        {
          "nickname": "lbh2****",
          "user_nick": "캐리왕짐캐리",
          "reply": "이제 중국입국 안막은걸 다른거 탓 못하겠구나. 이정부는 왜자꾸 핑계만 대냐 나중에 다 드러날걸",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "32",
          "hate": "4",
          "sentiment": "0.02"
        },
        {
          "nickname": "nice****",
          "user_nick": "JOHNNA",
          "reply": "포장박스 24시간? 택배 어떡하나...",
          "date": "2006-04-09",
          "re_reply_num": "3",
          "like": "26",
          "hate": "1",
          "sentiment": "0.03"
        },
        {
          "nickname": "a313****",
          "user_nick": "나른한오후",
          "reply": "에어로졸이면 마스크는 둘째치고 안구감염될판....",
          "date": "2006-04-09",
          "re_reply_num": "2",
          "like": "24",
          "hate": "0",
          "sentiment": "0.01"
        },
        {
          "nickname": "psk5****",
          "user_nick": "vlxjvos21",
          "reply": "건강하면 마스크 안쓰도 된다 고 씨부린늠이 민주당 이지.",
          "date": "2006-04-09",
          "re_reply_num": "1",
          "like": "26",
          "hate": "4",
          "sentiment": "0.82"
        },
        {
          "nickname": "tmtm****",
          "user_nick": "클리너디테일링",
          "reply": "에어로졸로 감염인즉슨.....면마스크 의미없고 kf80도 의미없음...kf94도 틈새없이 착용제대로 해야함.사회적거리두기도 의미없음...문재인,박능후...당장튀어와...신천지가 전부 서로얼굴에 침튀었겠니? 콜센타에서 서로 침이튀어서 감염됐겠니? 진작에 에어로졸이라는데 무능한 정부만 자꾸 비말이라 우겼자나!!!",
          "date": "2006-04-09",
          "re_reply_num": "3",
          "like": "22",
          "hate": "2",
          "sentiment": "0.01"
        },
        {
          "nickname": "sooj****",
          "user_nick": "향",
          "reply": "마스크 안 썼으면 엘리베이터 타지말고 걸어다녀.",
          "date": "2006-04-09",
          "re_reply_num": "1",
          "like": "20",
          "hate": "0",
          "sentiment": "0.12"
        },
        {
          "nickname": "fox3****",
          "user_nick": "fox3654",
          "reply": "중국에서 여러번 공기감염된다고 했었다... 정부는 아니라고 믿고싶었겠지",
          "date": "2006-04-09",
          "re_reply_num": "3",
          "like": "21",
          "hate": "2",
          "sentiment": "0.88"
        },
        {
          "nickname": "hyun****",
          "user_nick": "마루",
          "reply": "한국인들은 모두 중국코로나 라고 확신함.. 중국입국 금지 안시킨건 대역죄다",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "19",
          "hate": "0",
          "sentiment": "0.01"
        },
        {
          "nickname": "bboo****",
          "user_nick": "파워20",
          "reply": "건강하면 마스크 쓰지말라는게제일 무서움..",
          "date": "2006-04-09",
          "re_reply_num": "4",
          "like": "19",
          "hate": "2",
          "sentiment": "0.78"
        },
        {
          "nickname": "jons****",
          "user_nick": "jon",
          "reply": "참 재앙스럽네",
          "date": "2006-04-09",
          "re_reply_num": "1",
          "like": "30",
          "hate": "15",
          "sentiment": "0.01"
        },
        {
          "nickname": "miss****",
          "user_nick": "mis",
          "reply": "황사도 있고, 산업화로 인한 대기 오염이 날로 심각한 중국 입장에, 계속된 바이러스 발생이 억울하겠어요. 황당할 듯..이번에 우리도 중국이랑 엮어져 전세계 민폐국이란 오명을 썼는데요. 코로나가 사정 봐주는 것도 아니구. 다음번엔 꾀돌이 대만처럼 합시다. 1.발병지 입국금지! 2. 마스크 수출 금지 3. 휴교령. 4. 마스크 5부제... 어느새 앙상한 가지에 하얀 마스크 꽃이네요.목련인가? 생애 가장 고요한 봄맞이입니다. 여러분, 건강하세요~",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "15",
          "hate": "1",
          "sentiment": "0.0"
        },
        {
          "nickname": "nike****",
          "user_nick": "Discount",
          "reply": "문재인 입은 하수구다",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "12",
          "hate": "1",
          "sentiment": "0.68"
        },
        {
          "nickname": "yttf****",
          "user_nick": "어느봄날",
          "reply": "카드보드에서 24시간이니 택배박스에서 24시간 살아있다는거네..모두 택배조심..플라스틱이나 스탠레스에선 3일동안이나 살아있다니..택배받으시거든 소독약 뿌려서 어디 구석에 처받아놓고 3일이후에나 만져야 할듯..공기전염된다니 정부를 믿고 건강한사람은 마스크안써도 된다는 말은 믿어서는 안됨..정부 잘하고 있단 개솔은 니들끼리나 해주세요..ㅋ",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "11",
          "hate": "0",
          "sentiment": "1.0"
        },
        {
          "nickname": "vi_p****",
          "user_nick": "vi_",
          "reply": "새삼스럽게~ 다 알고 있었음 그래서 중국발 입국 막으라고 했잖아요 우리도 시간벌었어야했는데... 참 안일해 이 정부는",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "11",
          "hate": "0",
          "sentiment": "0.94"
        },
        {
          "nickname": "muda****",
          "user_nick": "해인",
          "reply": "내 그럴 줄 알았지 에어로졸 아니면 이렇게 급속도로 확산될 수가 없지... 과잉대응? 이럴땐 그게 현명한거지",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "11",
          "hate": "1",
          "sentiment": "0.01"
        },
        {
          "nickname": "kwon****",
          "user_nick": "47은순아들200108n7",
          "reply": "환기가 안되는 지하공간이나 밀폐된 공간은 가지 않는게 상책이라는거네...",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "10",
          "hate": "0",
          "sentiment": "0.04"
        },
        {
          "nickname": "koda****",
          "user_nick": "무한돌파",
          "reply": "근데 이게 사실이라면 전국민 다 감염됐다해도 안이상하지않나...",
          "date": "2006-04-09",
          "re_reply_num": "2",
          "like": "10",
          "hate": "1",
          "sentiment": "0.04"
        },
        {
          "nickname": "drea****",
          "user_nick": "dre",
          "reply": "중국의 코로나 중국에서 발병된거 100%인데 정보도 공개 안하고 8만명이라는데 그거 뻥이다 최소 20만이다~ 그리고 지금 코로나 공정 들어갔다... 자기들 책임 아니고 한국,미국이라고 떠들어댄다~ 믿지 말자 가짜정보",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "9",
          "hate": "1",
          "sentiment": "0.97"
        },
        {
          "nickname": "runa****",
          "user_nick": "듀나메스",
          "reply": "택배상자가 위험해ㆍ",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "9",
          "hate": "1",
          "sentiment": "0.1"
        },
        {
          "nickname": "natj****",
          "user_nick": "nat",
          "reply": "연합뉴스는 도대체 뉴스하는 목적이 무엇인가요?팩트를 알리는건가요, 불안을 조장하는건가요?출연하신 의사분이 환기가 전혀 안되는 공간안에서 특정 온도일때 바이러스의 12.5%가 3시간동안 남아있었다. 이 말은 90%정도는 사라졌다고 보면 된다.아주 특정온도에 있을때라고 즉 그런 연구가 있다고 흘려들으면 된다고 분명히 말씀하시는데 밑에 자막으로 \"3시간 존재\"라고 대문짝만하게 내보는데 기가 막힌다~!!!!! 말귀를 못알아듣는건가, 시청자를 등신으로 아는건가~!!! 도대체 뉴스가 왜 이모양인가~!!!!뉴스 좀 제대로 듣자~!!!",
          "date": "2006-04-09",
          "re_reply_num": "2",
          "like": "11",
          "hate": "4",
          "sentiment": "0.0"
        },
        {
          "nickname": "hapo****",
          "user_nick": "vanillecremebrulee",
          "reply": "정부가 하는 것마다 다 엇나가는구만... 17세 청소년 죽은건 어떻게 설명할거며?기저질환이 있든 없든 젊든 늙었던 모든 생명이 다 귀하다... 세월호에서 희생된 아이들한테 고맙다던 악마가 대통령이 되서 그런가? 누가 걸리던 죽던 중국 눈치만 보고 일본만 걸고 넘어지고 자화자찬만 해대면 다인가??",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "9",
          "hate": "2",
          "sentiment": "0.96"
        },
        {
          "nickname": "firs****",
          "user_nick": "빵이",
          "reply": "홍콩이나 몽골좀 본받자. 감염초기부터 완전 국경폐쇠하면서 감염률 최소치를 보이지 않냐? 우리나라는 문 활짝 열어 놓더라",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "7",
          "hate": "0",
          "sentiment": "0.53"
        },
        {
          "nickname": "siyu****",
          "user_nick": "siy",
          "reply": "공기감염이라니...",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "7",
          "hate": "0",
          "sentiment": "0.22"
        },
        {
          "nickname": "palm****",
          "user_nick": "palmball21",
          "reply": "1번 중국확진자 나오고 중국서 중국인29만,내국인10만 단순열체크만하고 왕래했다 ᆢ 일본크루즈도 홍콩노인네 하나로 시작됐고 전문가집단 일관된 목소리로 말했었고 ㅡㅡ 오늘 17세 청소년도 마스크사러댕기다 ᆢ 아놔 진짜 빙삼정부니들은 진짜 인간도아니다 짜파구리나 먹고 북한북한소리나 해라",
          "date": "2006-04-09",
          "re_reply_num": "1",
          "like": "10",
          "hate": "4",
          "sentiment": "0.05"
        },
        {
          "nickname": "rlaw****",
          "user_nick": "Xuicide",
          "reply": "미국 cdc 오피셜 난거니까 이제 가짜뉴스 타령도 못하겠네?문재인 못믿어서 이미 고글이랑 방독면 사놨다 나갈때는 무조건 이거 차고나감",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "7",
          "hate": "1",
          "sentiment": "0.02"
        },
        {
          "nickname": "sime****",
          "user_nick": "JADU",
          "reply": "그럼 선별진료소에소 여러명이서 입벌리고 검사받는건 안위험한가요? ㅜㅜ 한명하고 소독하는곳도 잘 없던데",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "6",
          "hate": "0",
          "sentiment": "0.04"
        },
        {
          "nickname": "m45f****",
          "user_nick": "딸기맛우유",
          "reply": "엘리베이터 엄청 위험하네",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "6",
          "hate": "0",
          "sentiment": "0.64"
        },
        {
          "nickname": "tmtm****",
          "user_nick": "클리너디테일링",
          "reply": "무건 비말감염이라고 정부가 우기는바람에 에꿋은 자원봉사자들은 지금도 열심히 재봉틀굴리며 면마스크 만들고있습니다...애초에 공기감염이라했자나요...kf94아니면 못막아요...그조차 빈틈없이 제대로 착용해야 막을수있구요...무튼 마스크대란부터 지오영까지...끝까지 심판받을 각오하세요",
          "date": "2006-04-09",
          "re_reply_num": "2",
          "like": "7",
          "hate": "2",
          "sentiment": "0.1"
        },
        {
          "nickname": "rpg1****",
          "user_nick": "rpg",
          "reply": "한가지 확실한점은 마스크를 쓰면 괜찮다는거...확진자인지 모르니까 전부 마스크 쓰세요 기침을 해도 본인 마스크에만 묻을테니",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "5",
          "hate": "0",
          "sentiment": "0.01"
        },
        {
          "nickname": "syeu****",
          "user_nick": "감사",
          "reply": "사회복지사 보건복지부장관 둬서 무증상감염10%인데 없다고했었고, 우한방문 14일내 유증상자만 검사할 수 있게하고 중국발 항공기 올패스시켜 내외국인 막 다녀서 판데믹에 일조한 나라 우한코로나라고 못하는 중국속국되었다. 면마스크, 일회용재사용, 사회적 거리두면 괜찮다 했는 국민살상 대한민국 문제인 대통령의 더불어공산당 정부는 모든 책임을 지고 물러나라!! 무능한 민주당원으로만 나라일을 하니 통역사 외교부장관, 민주당일하는 법무부장관, 교육무관 병역기피 위장전입 교육부장관 등으로 부동산.안보.경제 더불어 모든 분야를 망쳤다 #민주당만빼고",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "5",
          "hate": "0",
          "sentiment": "0.0"
        },
        {
          "nickname": "gydu****",
          "user_nick": "gyd",
          "reply": "바이러스가 무서운게 활동이 잠식된거지 죽은게 아니란말이지 언제든 조건이 맞고 숙주만있으면 살아난다는 건데 코로나말고도 아직 치료제도 없는 바이러스들이 떠돌고 있을텐데 휴...어찌됐든인류는 또 진화하겠지.. 다음세대들은 면역력이 있기를..",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "5",
          "hate": "0",
          "sentiment": "0.69"
        },
        {
          "nickname": "wind****",
          "user_nick": "Jiu",
          "reply": "비말이라고 할때부터 내 머릿속에는 에어로졸로 인지하고 있었음. 침방울은 1+1의 개념. 생각해봐라. 감기걸린 사람이 내 얼굴에 침 안튀어도 같은 공간 사무실 쓰면 죄다 콜록대기 시작한다. 최소 감기수준도 이런데 비말이 굳이 면상때기에 침튀었다고 코로나 전염되냐고. 이전까지 걸린 양상을 보면 대화도 안한 사람들 다 걸리고. 이건 공기전파잖어.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "5",
          "hate": "0",
          "sentiment": "0.49"
        },
        {
          "nickname": "outl****",
          "user_nick": "기상청",
          "reply": "3시간 와 .. ㅈ되네 진짜. 중국 진짜 핵미사일로 없애버리고싶다..",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "5",
          "hate": "0",
          "sentiment": "0.6"
        },
        {
          "nickname": "fore****",
          "user_nick": "만식이엄마",
          "reply": "호흡기 바이러스가 공기중감염 안된다는게 이상한거지",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "5",
          "hate": "0",
          "sentiment": "0.04"
        },
        {
          "nickname": "taek****",
          "user_nick": "단무지",
          "reply": "중국이 초반에 감추지만 않았어도.WHO가 적극적으로 대처만 했어도.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "5",
          "hate": "0",
          "sentiment": "0.21"
        },
        {
          "nickname": "jaso****",
          "user_nick": "왕대천사",
          "reply": "듣고싶은것만 골라듣고 차이나게이트, 마스크게이트는 은폐하고 문재인 정부는 진짜 재앙이고 노답이다..",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "6",
          "hate": "2",
          "sentiment": "0.02"
        },
        {
          "nickname": "psm4****",
          "user_nick": "psm",
          "reply": "미국이 이런 연구 발표하면 뭐하나 마스크도 안끼고 디즈니에서 종강파티여는 사람들인데....",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "4",
          "hate": "0",
          "sentiment": "0.14"
        },
        {
          "nickname": "imcd****",
          "user_nick": "imc",
          "reply": "그러면서도 마스크안꺼도 된다고 하는 미국정부도 참.. 여기 미국인데 마스크 안껴요... 무서워서 못나가겠음",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "4",
          "hate": "0",
          "sentiment": "0.06"
        },
        {
          "nickname": "catd****",
          "user_nick": "하얀괭이",
          "reply": "한국이 세계 최고의 의료대책으로 대응하고 있는건 팩트",
          "date": "2006-04-09",
          "re_reply_num": "4",
          "like": "8",
          "hate": "5",
          "sentiment": "0.86"
        },
        {
          "nickname": "kkeg****",
          "user_nick": "콩꼬막",
          "reply": "에어로졸이 전혀 감염이 안된다고 안한것 같은데. 그것보단 접촉이 더 잘된다고 사회적 거리두기가 중점이라 했던것 같은데. 다들 뉴스보면서 다른생각한건가??? 같은 가족이라도 각자방쓰고 화장실도 따로 쓰고하라했잖아요. 에어로졸 가능이 있으니 환기도 따로 하라고. 그러나 접촉이 더 감염이 잘되니 손잘씻고 마스크도 하라고.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "4",
          "hate": "1",
          "sentiment": "0.0"
        },
        {
          "nickname": "300c****",
          "user_nick": "나야나",
          "reply": "결국 백신개발만이 살길이네",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "3",
          "hate": "0",
          "sentiment": "0.03"
        },
        {
          "nickname": "chwh****",
          "user_nick": "jch89",
          "reply": "에어로졸 전파 우린 이미 알고있다 이미 코로나 바이러스 근원지인 중국의 입장에서 나왔는데 뭘 새삼스레 엄청난 사실을 알아낸 것처럼....그것도 뒷북으로...근데 3시간이씩이나? ㅎㄷㄷㄷ",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "3",
          "hate": "0",
          "sentiment": "0.17"
        },
        {
          "nickname": "sbbt****",
          "user_nick": "Travis",
          "reply": "중국 우한폐렴",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "3",
          "hate": "0",
          "sentiment": "0.2"
        },
        {
          "nickname": "7icr****",
          "user_nick": "하로",
          "reply": "역시 에어로졸이니 신천지 사람도 그렇게 많이 감염됐지 ..ㄷㄷ.. 지금 대형교회나 모임 클럽 등등 사람 많은곳은 피해야한다. 한사람 걸려도 파장이ㅜㅜ..대구 힘내세요. 이건 입국금지가 답이었어. 대륙남tv보면서 우한폐렴의 심각성을 느끼고 있었는데 공중에서 3시간 살아있다니 소름이다ㅠㅠ 어디나가지 말고 집에 있는게 답ㅜㅜ",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "3",
          "hate": "0",
          "sentiment": "1.0"
        },
        {
          "nickname": "pice****",
          "user_nick": "레비앙",
          "reply": "ktx 괜찮은건가요.. ?ㄷㄷ.. 다음주에 타고 가야하는데 ;;",
          "date": "2006-04-09",
          "re_reply_num": "2",
          "like": "3",
          "hate": "0",
          "sentiment": "0.94"
        },
        {
          "nickname": "rldb****",
          "user_nick": "rld",
          "reply": "중국 공산당의 의도적인 전세계를 겨냥한 생화학 테러 행위 입니다 전세계는 중국에 보복을 해야합니다",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "3",
          "hate": "0",
          "sentiment": "0.8"
        },
        {
          "nickname": "ss86****",
          "user_nick": "귀요미",
          "reply": "뭐든 넓게 크게봐야죠비말감염이 진짜100프로로 장담할수도없으며많은사람들이ㅈ쉽게쉽게 감염이되니뭐든조심하고 주의하는게 좋다고봅니다1프로의 확률도 무시할수없습니다공포감조성이딴거 뭐가중요한가요?지금 사망자가 100명이다되어가고 앞으로계속나올것이고이제 딱 가둬두고정해놓은 신천지인원검사끝난거면이제 진짜 어디서감염된지 모르는 일반인들이나올텐데 그게 더무섭습니다공포감을줘서라도 조심하고또조심해야 할때입니다",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "3",
          "hate": "0",
          "sentiment": "0.0"
        },
        {
          "nickname": "ttun****",
          "user_nick": "스카이워커",
          "reply": "팩트 ㅡ 현 kf94로는 에어로졸 못막음 다만 침방울 비말만 걸러냄 따라서 재채기 기침 하는 사람과 밀페장소는 마스크 써도 걸림",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "3",
          "hate": "0",
          "sentiment": "0.84"
        },
        {
          "nickname": "ceod****",
          "user_nick": "DODOceo",
          "reply": "백신좀빨리만들어주세요",
          "date": "2006-04-09",
          "re_reply_num": "1",
          "like": "3",
          "hate": "1",
          "sentiment": "0.19"
        },
        {
          "nickname": "ices****",
          "user_nick": "삐삐",
          "reply": "정부가 아니라고 우겼던게 다 사실로 밝혀지고 있다.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "2",
          "hate": "0",
          "sentiment": "0.38"
        },
        {
          "nickname": "pjis****",
          "user_nick": "용감한 수호자",
          "reply": "에어로졸 감염이 된다면 마스크도 아무 소용없고 의료진들 입는 방호복인지 우주복 같은거 입어야 안걸리는거 아닌가요?? 이 기사 팩트라면 심각하네요",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "2",
          "hate": "0",
          "sentiment": "0.25"
        },
        {
          "nickname": "cj86****",
          "user_nick": "보스베이비",
          "reply": "문재인 어디갔냐",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "2",
          "hate": "0",
          "sentiment": "0.49"
        },
        {
          "nickname": "mill****",
          "user_nick": "millenniumna",
          "reply": "공기중 감염 인정하고 대책 세워서 코로나 무찔러 주세요~투명하게 인정하고 해결합시다.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "2",
          "hate": "0",
          "sentiment": "0.2"
        },
        {
          "nickname": "smbe****",
          "user_nick": "초코아이스크림",
          "reply": "암튼 에어로졸 맞네 자꾸 숨기려들지마라 더 악화될뿐이다정직하게 발표해야 더 조심하지",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "2",
          "hate": "0",
          "sentiment": "0.77"
        },
        {
          "nickname": "jpop****",
          "user_nick": "Zzoo",
          "reply": "10프로 무증상 감염자인 짱개가 얼마나 퍼뜨리고 다녔을거야..무섭다.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "2",
          "hate": "0",
          "sentiment": "0.01"
        },
        {
          "nickname": "tmtm****",
          "user_nick": "클리너디테일링",
          "reply": "그러게 비말아니고 공기감염이라니까!! 그렇게 거짓에 선동되지말람서? 생각을쫌해라정부야...신천지가 같이예배하면서 서로얼굴에 침이다튀었겠니? 진짜 생각없이 마구 나불대는 문정부...",
          "date": "2006-04-09",
          "re_reply_num": "2",
          "like": "3",
          "hate": "2",
          "sentiment": "0.01"
        },
        {
          "nickname": "chem****",
          "user_nick": "che",
          "reply": "우리 보건당국 수준이 중국보다 떨어지나 보네. 살기위해 정치에 줄서다 보니 불리한 사실을 축소 또는 왜곡하려는 것 같은데 이해는 가네.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "3",
          "hate": "2",
          "sentiment": "0.61"
        },
        {
          "nickname": "halb****",
          "user_nick": "Me",
          "reply": "아니 에어로졸 안된다며요..진짜 뭐하자는거야..?에어로졸이면 면마스크 안되는거 아닌가요???저 면마스크 쓰고 지하철 아침저녁으로 타고다니는데 --이번주 주말에 줄서로 가야겠네요..",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "2",
          "hate": "1",
          "sentiment": "0.03"
        },
        {
          "nickname": "jshy****",
          "user_nick": "노부농",
          "reply": "헐 시이팔 ㅈ됐네",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "2",
          "hate": "1",
          "sentiment": "0.03"
        },
        {
          "nickname": "bgyn****",
          "user_nick": "Digil",
          "reply": "공기중에 감염되니까 이렇게 퍼지지 모두 우주복 입고 다녀라",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "2",
          "hate": "1",
          "sentiment": "0.88"
        },
        {
          "nickname": "ips4****",
          "user_nick": "ips",
          "reply": "중국때문에 다망했다 특히 우리 한국은 아직도 밑이 안보인더",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "1",
          "hate": "0",
          "sentiment": "0.71"
        },
        {
          "nickname": "woor****",
          "user_nick": "하루하루",
          "reply": "결국은 전 안류를 감염시키고서야 끝이 나겠네",
          "date": "2006-04-09",
          "re_reply_num": "1",
          "like": "1",
          "hate": "0",
          "sentiment": "0.26"
        },
        {
          "nickname": "bmwx****",
          "user_nick": "냉동학철학",
          "reply": "어쩐지...공기중이라면 .심각한건데.전인류는 어쩌나요?",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "1",
          "hate": "0",
          "sentiment": "0.18"
        },
        {
          "nickname": "shm1****",
          "user_nick": "sun",
          "reply": "버스나 사무실이나 가게낮공기순환되게 환기좀자주 시켜주세요~특히 버스",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "1",
          "hate": "0",
          "sentiment": "0.63"
        },
        {
          "nickname": "bbip****",
          "user_nick": "에비츄",
          "reply": "나 몇주전 뉴스에서 봤을땐 박스에선 코로나바이러스가 몇십분밖에 못산다고 봤는데 뭐가 진실인거냐??",
          "date": "2006-04-09",
          "re_reply_num": "1",
          "like": "1",
          "hate": "0",
          "sentiment": "0.01"
        },
        {
          "nickname": "rlad****",
          "user_nick": "rladustn1201",
          "reply": "중국바이러스 너무 무섭다...",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "1",
          "hate": "0",
          "sentiment": "0.3"
        },
        {
          "nickname": "bnwo****",
          "user_nick": "진검",
          "reply": "미국 끝장날 듯 유럽에서 수일간 복귀한 그 많은 사람들 공항에서 마스크 안끼고 수많은 사람들이 빼곡히 수시간 많게는 열시간, 신천지보다 더 빼곡히 그 수만은 사람들이 슈퍼전파자 컥",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "1",
          "hate": "0",
          "sentiment": "0.79"
        },
        {
          "nickname": "ceod****",
          "user_nick": "DODOceo",
          "reply": "언제쯤 끝날까요 ..",
          "date": "2006-04-09",
          "re_reply_num": "1",
          "like": "1",
          "hate": "0",
          "sentiment": "0.63"
        },
        {
          "nickname": "pjm3****",
          "user_nick": "느어어어",
          "reply": "중국에서 만든 생화학무기 아니냐진짜??",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "1",
          "hate": "0",
          "sentiment": "0.07"
        },
        {
          "nickname": "youm****",
          "user_nick": "you",
          "reply": "삐빅~~ 또 문재인정권에의해 가짜뉴스로 매도될소식입니다.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "1",
          "hate": "0",
          "sentiment": "0.19"
        },
        {
          "nickname": "punk****",
          "user_nick": "런던",
          "reply": "안된다고 마스크 꼭 안껴도 된다고 했죠?",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "1",
          "hate": "0",
          "sentiment": "0.33"
        },
        {
          "nickname": "didr****",
          "user_nick": "did",
          "reply": "언제쯤 끝나려나",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "1",
          "hate": "0",
          "sentiment": "0.12"
        },
        {
          "nickname": "jrki****",
          "user_nick": "좋은사람",
          "reply": "택배도 속독해라.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "1",
          "hate": "0",
          "sentiment": "0.09"
        },
        {
          "nickname": "jj28****",
          "user_nick": "jj2",
          "reply": "이제 방독면 쓰고 다니라는 거냐?",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "1",
          "hate": "0",
          "sentiment": "0.09"
        },
        {
          "nickname": "crei****",
          "user_nick": "Tran",
          "reply": "중국 새끼들 한테 나온거라 그런지 코로나 바이러스도 개때구나",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "1",
          "hate": "0",
          "sentiment": "0.03"
        },
        {
          "nickname": "tlac****",
          "user_nick": "tlacogk",
          "reply": "거짓으로 지금까지 이지경만든 정부중국 못막고 근본적인 책임 신천지 대구한테 돌리고 지금까지 왔어 자 지금 유럽도 안막고 이번에는 누구한테 책임 떠넘기래",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "1",
          "hate": "1",
          "sentiment": "0.01"
        },
        {
          "nickname": "form****",
          "user_nick": "bo",
          "reply": "공식명칭 코로나19",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "1",
          "hate": "1",
          "sentiment": "0.06"
        },
        {
          "nickname": "xodo****",
          "user_nick": "xod",
          "reply": "이거 원문 기사 어떻게 찾을 수 있죠? 외국에 사는데 외국 사람들한테 보여주고 싶어서요. 저기 사이트랑 구글링 해도 안나오네요",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.01"
        },
        {
          "nickname": "amur****",
          "user_nick": "amu",
          "reply": "마스크써도 눈으로 감염될수있겠네...",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.07"
        },
        {
          "nickname": "noti****",
          "user_nick": "씀바귀",
          "reply": "서울사람 만나면 안되겠네요. 땅비좁은데 900만명 ㄷ ㄷ",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.86"
        },
        {
          "nickname": "dmee****",
          "user_nick": "LYSLMS",
          "reply": "이래도 마스크 안 쓸래? 서구권?",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.06"
        },
        {
          "nickname": "rin2****",
          "user_nick": "좋은하루",
          "reply": "공기 감염이면 여타 일반 독감 바이러스들과는 완전히 다른 전염 경로와 전염력을 가졌겠네ㅜㅜ",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.86"
        },
        {
          "nickname": "kot7****",
          "user_nick": "kot",
          "reply": "에어로졸 예방은 마스크 착용으로 예방이 가능합니다 ᆢ",
          "date": "2006-04-09",
          "re_reply_num": "1",
          "like": "0",
          "hate": "0",
          "sentiment": "0.43"
        },
        {
          "nickname": "zzan****",
          "user_nick": "지지아나",
          "reply": "이거 정말 백신개발만이 종식될 수 있는 유일한 해결책일수도... 정말 심각하네",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.04"
        },
        {
          "nickname": "ssiw****",
          "user_nick": "슈다",
          "reply": "엘레베이터 감염자가 에어로졸에 감염된게 맞는거지 무슨 손을 비비고 입에 가져다 댔느니.. 호흡에도 미립자 검출되는지 검사바랍니다.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.49"
        },
        {
          "nickname": "ices****",
          "user_nick": "삐삐",
          "reply": "부산 확진자중 무증상 확진자가 10프로라고 기사 떴음. 중국과 일치. 발열체크 열심히 한다며 무증상감염도 끝까지 인정안했지.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.14"
        },
        {
          "nickname": "chun****",
          "user_nick": "Sky Go",
          "reply": "에어졸에 속독약 없이 사용한곳이 문제였다.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.36"
        },
        {
          "nickname": "sjb3****",
          "user_nick": "옹박",
          "reply": "결국 황사로도 감염됨. 헐 재수없으면 골로가겠네.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.03"
        },
        {
          "nickname": "dkdl****",
          "user_nick": "쥬므란",
          "reply": "결론 공기전파 된다 알겠음",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.11"
        },
        {
          "nickname": "bamb****",
          "user_nick": "크르릉",
          "reply": "이거 진짜 심각한 일 아니냐..아파트같은데 중국에서 사스인가? 에어로졸때문에 층간 감염된 사례있든데",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.02"
        },
        {
          "nickname": "kot7****",
          "user_nick": "kot",
          "reply": "상시 히잡을 써야 할 듯 ᆢ",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.19"
        },
        {
          "nickname": "smj1****",
          "user_nick": "haha",
          "reply": "공기감염...뜨악....이동시 잠깐타는 엘르베이터도?? 걸어서 내려가야 되나...ㅜ ㅠ",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.3"
        },
        {
          "nickname": "kot7****",
          "user_nick": "kot",
          "reply": "마스크를 일상화 하지 않을 수 없는 이유가 발견되었군요 ᆢ앞으로는 자연스레 마스크시위가 합법적이 되었습니다.그렇게 얼굴가리고 시위할 수 있도록 해 달라고 발광하더구만얼굴 들어내기를 두려워하는 문빠세력들 ᆢ어찌하든 마스크는 휴대합시다.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "1.0"
        },
        {
          "nickname": "fore****",
          "user_nick": "만식이엄마",
          "reply": "쉽게생각해서 멍멍이들만 봐도 디스템퍼.코로나는 왜 입원치료를 권하지 않을까요?격리실이 잇어도.공기중으로 전염가능하기에.장기간의 치료가 필요하기에 입원치료 권하지 안아요.반면.개파보.켄넬코프같은 바이러스는 접촉성이기에 입원치료가 가능한거에요 모두가아주심각한 바이러스지만.공기중.접촉성에따른 취사율 무시못함이죠.둘다 일주일에서 14일 잠복기간이잇고 .반반의완치 때문입니다.개는개고 사람은 사람이다 따지기전에 정확한 바이러스이동을 알아내는게 맞는것같네요",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.92"
        },
        {
          "nickname": "jang****",
          "user_nick": "jan",
          "reply": ".",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.44"
        },
        {
          "nickname": "zxco****",
          "user_nick": "zxc",
          "reply": "클린봇이 부적절한 표현을 감지한 댓글입니다.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.88"
        },
        {
          "nickname": "shm1****",
          "user_nick": "sun",
          "reply": "소독제도 환기되는곳에서 사용해야함밀폐된 공간에서 흡입하면 위험한거알고있겠지 기본상식인데~",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.94"
        },
        {
          "nickname": "dlfn****",
          "user_nick": "dlf",
          "reply": "아니 어쩌라는거야 진짜이거 진짜 심각한데진짜 심각해",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.06"
        },
        {
          "nickname": "kanv****",
          "user_nick": "kan",
          "reply": "비말 감염만 주의하면 될거라고 생각했었는데 3일 생존? 심각하네.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.17"
        },
        {
          "nickname": "eunj****",
          "user_nick": "Alice Eunju Kim",
          "reply": "그럼 택배나 배달품은?",
          "date": "2006-04-09",
          "re_reply_num": "2",
          "like": "0",
          "hate": "0",
          "sentiment": "0.06"
        },
        {
          "nickname": "hyea****",
          "user_nick": "MINE",
          "reply": "택배 자제하세요. 택배상자에 묻어있을수 있어서 불안.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.44"
        },
        {
          "nickname": "hell****",
          "user_nick": "hellopinky02",
          "reply": "마스크 줄서기도 무서워지네요ㅜㅜ",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.56"
        },
        {
          "nickname": "trw2****",
          "user_nick": "준이",
          "reply": "역적",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.46"
        },
        {
          "nickname": "qhrt****",
          "user_nick": "브레인",
          "reply": "이거 누구 만나는것도 무섭다...",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.27"
        },
        {
          "nickname": "hair****",
          "user_nick": "디자이너현민",
          "reply": "공기감염 어찌 막을건데 ,,;; 이산화염소 목걸이 효과없다며(공간제균) 공기감염 대책마련해주세요",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.52"
        },
        {
          "nickname": "chan****",
          "user_nick": "최강젖히기",
          "reply": "클린봇이 부적절한 표현을 감지한 댓글입니다.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.88"
        },
        {
          "nickname": "yous****",
          "user_nick": "츄츄",
          "reply": "클린봇이 부적절한 표현을 감지한 댓글입니다.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.88"
        },
        {
          "nickname": "zzan****",
          "user_nick": "설현남편",
          "reply": "클린봇이 부적절한 표현을 감지한 댓글입니다.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.88"
        },
        {
          "nickname": "lhs0****",
          "user_nick": "lhs",
          "reply": "소독용 에탄올 분무기에 넣어서 뿌리는건 괜찮쥬?",
          "date": "2006-04-09",
          "re_reply_num": "2",
          "like": "0",
          "hate": "0",
          "sentiment": "0.04"
        },
        {
          "nickname": "sldr****",
          "user_nick": "sldrjaak",
          "reply": "예상확진환자 25000명에 안타깝지만 학생의경우는 코로나 유전자변이에 의한 사망으로 나이가많든적든중요한게 아니고 걸리믄 반드시 암처럼 몸에 갖고있으며 합병증의위험 재확진의 가능성 및 완치하여도 폐는 이미 죽어있다는것...",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.0"
        },
        {
          "nickname": "endo****",
          "user_nick": "endo",
          "reply": "걸을때 마스크 안쓰도 된다며?",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.09"
        },
        {
          "nickname": "haro****",
          "user_nick": "제자리걸음",
          "reply": "마스크 꼭 껴야겠네.....무조건........",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.44"
        },
        {
          "nickname": "skam****",
          "user_nick": "ska",
          "reply": "ㅈ됬다이거",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.19"
        },
        {
          "nickname": "lmw0****",
          "user_nick": "토끼풀잎",
          "reply": "사무실 ,가게안,엘리베이터 안에서 20~30분에 한번씩 알콜80%소독제 뿌리고 5~10분씩 창문열어서 환기하고 마스크 착용하고 일해야 된다는거,손도 씻고 알콜손소독제 한번씩, 먹고난 음식ᆞ택배박스에 코로나 살균제 뿌리고 버려야 되고 ,화장실도 한번씩 알콜80%소독제 뿌리고 환기해줘야 합니다.주의사항 , 서류에 알콜80% 소독제 닿으면 프린트된 글자가 사라집니다, 검정색 플라스틱은 회색으로 탈색 됩니다.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.0"
        },
        {
          "nickname": "thes****",
          "user_nick": "템파",
          "reply": "장난아니네",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.6"
        },
        {
          "nickname": "dlss****",
          "user_nick": "마음소리",
          "reply": "일찍 인정할건 인정하고 그에대한 대처를 해야 하는데....열심히 방역을 하지만은 코로나 감염자는 어디에든 숨어있을듯...",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.98"
        },
        {
          "nickname": "seon****",
          "user_nick": "콩냥",
          "reply": "확진자 생긴 동네,, 회사, 거의 무증상 감염자로 보아도 무방하겠네..확진자 지나간후 하루지나 다녀온 마트에서도 감염될수 있는거자나~~",
          "date": "2006-04-09",
          "re_reply_num": "1",
          "like": "0",
          "hate": "0",
          "sentiment": "0.67"
        },
        {
          "nickname": "sdm1****",
          "user_nick": "sdm",
          "reply": "택배 하루 지나서 열어야 할듯",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.26"
        },
        {
          "nickname": "seah****",
          "user_nick": "sea",
          "reply": "하.. 이 질환을 몇명이나 피해갈 수 있을까 ㅜㅜㅜ",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.33"
        },
        {
          "nickname": "blue****",
          "user_nick": "블루드림",
          "reply": "대한민국 정부는 아무리 그래도 안믿는다. 왜? 경제도 살려야 하니깐 ㅎ",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.98"
        },
        {
          "nickname": "alsr****",
          "user_nick": "데이지킴",
          "reply": "청호나이스 필터교체 오지말라했는데 이제 잠잠해졌다면서 기어코 오는 사람 참 어이없네 한국사람들 참 어이없다 이렇게 대수롭지 않게 생각하니 이지경됐지ㅉㅉ 곱창집 줄서서 먹더라 불감증이니?",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.0"
        },
        {
          "nickname": "bast****",
          "user_nick": "프로필",
          "reply": "말이 에어로졸이지 밀폐된 곳에선 공기 감염이랑 다른게 거의 없네!!",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.9"
        },
        {
          "nickname": "kswo****",
          "user_nick": "워니",
          "reply": "마스크하고 손씻고 사회적거리두고 백신 나올때까지는 이런 생활 지속~~해야할듯~~요",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.08"
        },
        {
          "nickname": "iamr****",
          "user_nick": "김희주",
          "reply": "면마스크도 괜찮다고했던 문재인정부..",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.94"
        },
        {
          "nickname": "runu****",
          "user_nick": "미니멀",
          "reply": "처음엔 에어로졸 아니라며?",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.13"
        },
        {
          "nickname": "seon****",
          "user_nick": "이정현",
          "reply": "근데 왜 2호선 지하철안에서는 안나오는거지?! 신기한데",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.59"
        },
        {
          "nickname": "0111****",
          "user_nick": "011",
          "reply": "비말과 에어로졸이 다른거라니",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.56"
        },
        {
          "nickname": "fox3****",
          "user_nick": "fox3654",
          "reply": "그래서 버스기사 택시기사들도 감염됬던거지!!!",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.32"
        },
        {
          "nickname": "jch3****",
          "user_nick": "jch3057681",
          "reply": "공기중 감염이면 확진자옆에잇으면 당해낼 도리가 없네",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.67"
        },
        {
          "nickname": "stea****",
          "user_nick": "카일리",
          "reply": "공기감염되는데 ...정부는 안된다고 했는데",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.21"
        },
        {
          "nickname": "leag****",
          "user_nick": "좋은세상만들기",
          "reply": "새로운 신종코로나바이러스 인거야??? 아니면 코로나19 로 명칭된 바이러스를 이야기 하는거야?? 정확히 정보전달 부탁드립니다.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.13"
        },
        {
          "nickname": "stai****",
          "user_nick": "sta",
          "reply": "에어본이면 겁나 위험한거 아니가",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.45"
        },
        {
          "nickname": "kdss****",
          "user_nick": "와인",
          "reply": "교회에서 감염되는거보면 공기중으로 감염 가능한거 아닐까요?",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.78"
        },
        {
          "nickname": "ssal****",
          "user_nick": "ssalbob",
          "reply": "진짜 비닐모자 써야겠다.ㅠㅠ",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.97"
        },
        {
          "nickname": "fall****",
          "user_nick": "나의",
          "reply": "클린봇이 부적절한 표현을 감지한 댓글입니다.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "0",
          "sentiment": "0.88"
        },
        {
          "nickname": "ocea****",
          "user_nick": "사냥꾼",
          "reply": "재앙적인 세균이네",
          "date": "2006-04-09",
          "re_reply_num": "2",
          "like": "8",
          "hate": "9",
          "sentiment": "0.03"
        },
        {
          "nickname": "wind****",
          "user_nick": "Jiu",
          "reply": "이시국에 문재인 ���디갔냐? 국개의원들아 니들이 4월 15일에 선거하라며. 선거는 개뿔 어떻게 해? 누가 해? 니들 월급 받지마. 대깨문 저 물건이랑 정숙이 돼지 아줌마랑 만희랑 중국 우한으로 보내서 노후에 거기서 정착하시라하자. 진심 이시국에 대통령 지금 너 어디서 뭐하니? 나라 팔 궁리중이냐? 또 거짓말 시나리오 궁리냐? 정숙이는 대구가서 짜파구리라도 끓여날라. 세금 쳐쓰고선 하는게 하나도 없음",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "1",
          "sentiment": "0.0"
        },
        {
          "nickname": "rose****",
          "user_nick": "Cranky Rosen",
          "reply": "은에서는 바로 죽는 것 아닌가? 은을 사러 가야겠군!",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "1",
          "sentiment": "0.46"
        },
        {
          "nickname": "qeen****",
          "user_nick": "S",
          "reply": "택시 특히 창문 좀 열고 환기 좀 해주세요 창문안열고 마스크만 쓰면 끝??",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "1",
          "sentiment": "0.07"
        },
        {
          "nickname": "tlac****",
          "user_nick": "tlacogk",
          "reply": "이 미친정부 열받아지금 회사 식당들 다 닫아야됨 웃긴게 마스크끼고 밥먹을때 다 같이 식판들고 줄서서 어쩌면 소규모집단은 회사 식당일거다",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "2",
          "sentiment": "1.0"
        },
        {
          "nickname": "mgs0****",
          "user_nick": "mgs06049",
          "reply": "그렇게 욕하는 중국에서 나온게 조센민족 ㅋㅋㅋ 아 맞다 몽골한테도 ㄱㄱ 당했지?",
          "date": "2006-04-09",
          "re_reply_num": "2",
          "like": "0",
          "hate": "2",
          "sentiment": "0.02"
        },
        {
          "nickname": "touc****",
          "user_nick": "tou",
          "reply": "실험의 환경조건은 왜 말을 안하지? 분명 밀폐공간이고 특정한 온습도를 유지한 공간이었을텐데? 너무 공포심 유발시키지 말자 기자들아.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "2",
          "sentiment": "0.13"
        },
        {
          "nickname": "tkwk****",
          "user_nick": "tkw",
          "reply": "공중파는 문정부 앵무새입니다믿을수있는 유투브를 차라리 보세요퍼식이의 X파일 추천입니다",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "1",
          "hate": "4",
          "sentiment": "0.67"
        },
        {
          "nickname": "kimc****",
          "user_nick": "kim",
          "reply": "이런 기사를 왜 써서 혼란만 가중 시키는거지",
          "date": "2006-04-09",
          "re_reply_num": "2",
          "like": "0",
          "hate": "3",
          "sentiment": "0.11"
        },
        {
          "nickname": "kmhn****",
          "user_nick": "kmh",
          "reply": "Tk.입은하수구구나.댓글들마다 썩은냄새가 진동을하냐.제주모슬포인데 이제부터꼴통늙다리당 안찍는다.상대를비난하더라도 논리가앞서야지.운전하다빵구나도정부탓하면되냐.기생충tk당놈들아.",
          "date": "2006-04-09",
          "re_reply_num": "0",
          "like": "0",
          "hate": "6",
          "sentiment": "0.07"
        }
      ],
      headers2:[
        {
          text: 'Nickname',
          align: 'start',
          soratble: false,
          value: 'nickname'
        },
        { text: '활동명', value: 'user_nick' },
        { text: '활동 시작일', value: 'user_date' },
        { text: '총 댓글 개수', value: 'user_total_rp' },
        { text: '답글 수', value: 'user_response' },
        { text: '총 공감 수', value: 'user_sympathy' },
        { text: '작성', value: 'user_recent_write' },
        { text: '삭제', value: 'user_recent_delete' },
        { text: '공감', value: 'user_recent_sympathy' },
        { text: '받은 공감율', value: 'user_recent_sympathy_rate' },
        { text: '본인 삭제율', value: 'user_recent_delete_rate' }      
      ],
      "data2": [
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "602",
          "nickname": "pode****",
          "user_nick": "포대",
          "user_date": "2006-04-09",
          "user_history": "0.34",
          "user_total_rp": "16,247",
          "user_response": "313",
          "user_sympathy": "80,722",
          "user_recent_write": "149",
          "user_recent_delete": "63",
          "user_recent_sympathy": "92",
          "user_recent_sympathy_rate": "0.59",
          "user_recent_delete_rate": "0.42"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "603",
          "nickname": "mkba****",
          "user_nick": "자유가 아니면 죽음을",
          "user_date": "2006-04-09",
          "user_history": "0.53",
          "user_total_rp": "1,530",
          "user_response": "1,752",
          "user_sympathy": "15,971",
          "user_recent_write": "308",
          "user_recent_delete": "21",
          "user_recent_sympathy": "3238",
          "user_recent_sympathy_rate": "0.59",
          "user_recent_delete_rate": "0.07"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "604",
          "nickname": "5982****",
          "user_nick": "598",
          "user_date": "2006-04-09",
          "user_history": "0.3",
          "user_total_rp": "824",
          "user_response": "139",
          "user_sympathy": "4,323",
          "user_recent_write": "53",
          "user_recent_delete": "2",
          "user_recent_sympathy": "162",
          "user_recent_sympathy_rate": "0.87",
          "user_recent_delete_rate": "0.04"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "606",
          "nickname": "pkpk****",
          "user_nick": "pkp",
          "user_date": "2006-04-09",
          "user_history": "0.23",
          "user_total_rp": "2,028",
          "user_response": "414",
          "user_sympathy": "11,915",
          "user_recent_write": "140",
          "user_recent_delete": "6",
          "user_recent_sympathy": "233",
          "user_recent_sympathy_rate": "0.68",
          "user_recent_delete_rate": "0.04"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "607",
          "nickname": "hjsh****",
          "user_nick": "샤이니",
          "user_date": "2006-04-09",
          "user_history": "0.36",
          "user_total_rp": "794",
          "user_response": "683",
          "user_sympathy": "7,043",
          "user_recent_write": "84",
          "user_recent_delete": "1",
          "user_recent_sympathy": "222",
          "user_recent_sympathy_rate": "0.7",
          "user_recent_delete_rate": "0.01"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "608",
          "nickname": "lbh2****",
          "user_nick": "캐리왕짐캐리",
          "user_date": "2006-04-09",
          "user_history": "0.3",
          "user_total_rp": "393",
          "user_response": "26",
          "user_sympathy": "2,259",
          "user_recent_write": "12",
          "user_recent_delete": "0",
          "user_recent_sympathy": "28",
          "user_recent_sympathy_rate": "0.82",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "609",
          "nickname": "nice****",
          "user_nick": "JOHNNA",
          "user_date": "2006-04-09",
          "user_history": "0.36",
          "user_total_rp": "161",
          "user_response": "305",
          "user_sympathy": "72,653",
          "user_recent_write": "56",
          "user_recent_delete": "23",
          "user_recent_sympathy": "528",
          "user_recent_sympathy_rate": "0.83",
          "user_recent_delete_rate": "0.41"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "611",
          "nickname": "a313****",
          "user_nick": "나른한오후",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "27",
          "user_response": "6",
          "user_sympathy": "93",
          "user_recent_write": "9",
          "user_recent_delete": "1",
          "user_recent_sympathy": "16",
          "user_recent_sympathy_rate": "0.89",
          "user_recent_delete_rate": "0.11"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "612",
          "nickname": "psk5****",
          "user_nick": "vlxjvos21",
          "user_date": "2006-04-09",
          "user_history": "0.24",
          "user_total_rp": "5,424",
          "user_response": "3,242",
          "user_sympathy": "130,791",
          "user_recent_write": "534",
          "user_recent_delete": "23",
          "user_recent_sympathy": "4339",
          "user_recent_sympathy_rate": "0.8",
          "user_recent_delete_rate": "0.04"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "613",
          "nickname": "tmtm****",
          "user_nick": "클리너디테일링",
          "user_date": "2006-04-09",
          "user_history": "0.3",
          "user_total_rp": "398",
          "user_response": "109",
          "user_sympathy": "26,975",
          "user_recent_write": "92",
          "user_recent_delete": "7",
          "user_recent_sympathy": "1599",
          "user_recent_sympathy_rate": "0.78",
          "user_recent_delete_rate": "0.08"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "614",
          "nickname": "sooj****",
          "user_nick": "향",
          "user_date": "2006-04-09",
          "user_history": "0.34",
          "user_total_rp": "756",
          "user_response": "110",
          "user_sympathy": "8,393",
          "user_recent_write": "76",
          "user_recent_delete": "0",
          "user_recent_sympathy": "2723",
          "user_recent_sympathy_rate": "0.68",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "615",
          "nickname": "fox3****",
          "user_nick": "fox3654",
          "user_date": "2006-04-09",
          "user_history": "0.34",
          "user_total_rp": "1,344",
          "user_response": "144",
          "user_sympathy": "10,249",
          "user_recent_write": "166",
          "user_recent_delete": "1",
          "user_recent_sympathy": "1760",
          "user_recent_sympathy_rate": "0.88",
          "user_recent_delete_rate": "0.01"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "616",
          "nickname": "hyun****",
          "user_nick": "마루",
          "user_date": "2006-04-09",
          "user_history": "0.26",
          "user_total_rp": "136",
          "user_response": "2",
          "user_sympathy": "6,073",
          "user_recent_write": "78",
          "user_recent_delete": "51",
          "user_recent_sympathy": "340",
          "user_recent_sympathy_rate": "0.85",
          "user_recent_delete_rate": "0.65"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "618",
          "nickname": "bboo****",
          "user_nick": "파워20",
          "user_date": "2006-04-09",
          "user_history": "0.32",
          "user_total_rp": "375",
          "user_response": "1",
          "user_sympathy": "1,690",
          "user_recent_write": "116",
          "user_recent_delete": "0",
          "user_recent_sympathy": "361",
          "user_recent_sympathy_rate": "0.91",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "619",
          "nickname": "jons****",
          "user_nick": "jon",
          "user_date": "2006-04-09",
          "user_history": "0.24",
          "user_total_rp": "226",
          "user_response": "177",
          "user_sympathy": "1,237",
          "user_recent_write": "79",
          "user_recent_delete": "4",
          "user_recent_sympathy": "132",
          "user_recent_sympathy_rate": "0.49",
          "user_recent_delete_rate": "0.05"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "620",
          "nickname": "miss****",
          "user_nick": "mis",
          "user_date": "2006-04-09",
          "user_history": "0.49",
          "user_total_rp": "487",
          "user_response": "88",
          "user_sympathy": "5,321",
          "user_recent_write": "213",
          "user_recent_delete": "13",
          "user_recent_sympathy": "743",
          "user_recent_sympathy_rate": "0.83",
          "user_recent_delete_rate": "0.06"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "621",
          "nickname": "nike****",
          "user_nick": "Discount",
          "user_date": "2006-04-09",
          "user_history": "0.33",
          "user_total_rp": "1,205",
          "user_response": "174",
          "user_sympathy": "23,090",
          "user_recent_write": "217",
          "user_recent_delete": "120",
          "user_recent_sympathy": "7095",
          "user_recent_sympathy_rate": "0.67",
          "user_recent_delete_rate": "0.55"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "622",
          "nickname": "yttf****",
          "user_nick": "어느봄날",
          "user_date": "2006-04-09",
          "user_history": "0.36",
          "user_total_rp": "741",
          "user_response": "179",
          "user_sympathy": "4,378",
          "user_recent_write": "18",
          "user_recent_delete": "3",
          "user_recent_sympathy": "33",
          "user_recent_sympathy_rate": "0.83",
          "user_recent_delete_rate": "0.17"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "623",
          "nickname": "vi_p****",
          "user_nick": "vi_",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "3",
          "user_response": "10",
          "user_sympathy": "54",
          "user_recent_write": "1",
          "user_recent_delete": "0",
          "user_recent_sympathy": "11",
          "user_recent_sympathy_rate": "1.0",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "625",
          "nickname": "muda****",
          "user_nick": "해인",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "17",
          "user_response": "4",
          "user_sympathy": "33",
          "user_recent_write": "4",
          "user_recent_delete": "0",
          "user_recent_sympathy": "1",
          "user_recent_sympathy_rate": "1.0",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "626",
          "nickname": "kwon****",
          "user_nick": "47은순아들200108n7",
          "user_date": "2006-04-09",
          "user_history": "0.34",
          "user_total_rp": "3,271",
          "user_response": "66",
          "user_sympathy": "49,227",
          "user_recent_write": "31",
          "user_recent_delete": "1",
          "user_recent_sympathy": "163",
          "user_recent_sympathy_rate": "0.95",
          "user_recent_delete_rate": "0.03"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "627",
          "nickname": "koda****",
          "user_nick": "무한돌파",
          "user_date": "2006-04-09",
          "user_history": "0.33",
          "user_total_rp": "283",
          "user_response": "200",
          "user_sympathy": "4,275",
          "user_recent_write": "10",
          "user_recent_delete": "0",
          "user_recent_sympathy": "238",
          "user_recent_sympathy_rate": "0.98",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "628",
          "nickname": "drea****",
          "user_nick": "dre",
          "user_date": "2006-04-09",
          "user_history": "0.46",
          "user_total_rp": "367",
          "user_response": "130",
          "user_sympathy": "930",
          "user_recent_write": "16",
          "user_recent_delete": "0",
          "user_recent_sympathy": "52",
          "user_recent_sympathy_rate": "0.9",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "629",
          "nickname": "runa****",
          "user_nick": "듀나메스",
          "user_date": "2006-04-09",
          "user_history": "0.4",
          "user_total_rp": "1,515",
          "user_response": "781",
          "user_sympathy": "24,192",
          "user_recent_write": "54",
          "user_recent_delete": "1",
          "user_recent_sympathy": "156",
          "user_recent_sympathy_rate": "0.83",
          "user_recent_delete_rate": "0.02"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "630",
          "nickname": "natj****",
          "user_nick": "nat",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "9",
          "user_response": "35",
          "user_sympathy": "263",
          "user_recent_write": "16",
          "user_recent_delete": "0",
          "user_recent_sympathy": "34",
          "user_recent_sympathy_rate": "0.56",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "631",
          "nickname": "hapo****",
          "user_nick": "vanillecremebrulee",
          "user_date": "2006-04-09",
          "user_history": "0.22",
          "user_total_rp": "305",
          "user_response": "48",
          "user_sympathy": "1,669",
          "user_recent_write": "175",
          "user_recent_delete": "0",
          "user_recent_sympathy": "687",
          "user_recent_sympathy_rate": "0.82",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "632",
          "nickname": "firs****",
          "user_nick": "빵이",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "20",
          "user_response": "1",
          "user_sympathy": "39",
          "user_recent_write": "25",
          "user_recent_delete": "6",
          "user_recent_sympathy": "32",
          "user_recent_sympathy_rate": "0.63",
          "user_recent_delete_rate": "0.24"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "633",
          "nickname": "siyu****",
          "user_nick": "siy",
          "user_date": "2006-04-09",
          "user_history": "0.41",
          "user_total_rp": "329",
          "user_response": "1",
          "user_sympathy": "249",
          "user_recent_write": "171",
          "user_recent_delete": "1",
          "user_recent_sympathy": "108",
          "user_recent_sympathy_rate": "0.99",
          "user_recent_delete_rate": "0.01"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "634",
          "nickname": "palm****",
          "user_nick": "palmball21",
          "user_date": "2006-04-09",
          "user_history": "0.28",
          "user_total_rp": "3,026",
          "user_response": "1,658",
          "user_sympathy": "21,885",
          "user_recent_write": "106",
          "user_recent_delete": "0",
          "user_recent_sympathy": "371",
          "user_recent_sympathy_rate": "0.88",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "635",
          "nickname": "rlaw****",
          "user_nick": "Xuicide",
          "user_date": "2006-04-09",
          "user_history": "0.31",
          "user_total_rp": "545",
          "user_response": "130",
          "user_sympathy": "18,333",
          "user_recent_write": "131",
          "user_recent_delete": "24",
          "user_recent_sympathy": "12183",
          "user_recent_sympathy_rate": "0.94",
          "user_recent_delete_rate": "0.18"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "637",
          "nickname": "sime****",
          "user_nick": "JADU",
          "user_date": "2006-04-09",
          "user_history": "0.32",
          "user_total_rp": "1,379",
          "user_response": "333",
          "user_sympathy": "14,811",
          "user_recent_write": "48",
          "user_recent_delete": "0",
          "user_recent_sympathy": "453",
          "user_recent_sympathy_rate": "0.97",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "638",
          "nickname": "m45f****",
          "user_nick": "딸기맛우유",
          "user_date": "2006-04-09",
          "user_history": "0.32",
          "user_total_rp": "1,133",
          "user_response": "618",
          "user_sympathy": "13,028",
          "user_recent_write": "216",
          "user_recent_delete": "8",
          "user_recent_sympathy": "646",
          "user_recent_sympathy_rate": "0.83",
          "user_recent_delete_rate": "0.04"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "639",
          "nickname": "tmtm****",
          "user_nick": "클리너디테일링",
          "user_date": "2006-04-09",
          "user_history": "0.3",
          "user_total_rp": "398",
          "user_response": "109",
          "user_sympathy": "26,975",
          "user_recent_write": "92",
          "user_recent_delete": "7",
          "user_recent_sympathy": "1599",
          "user_recent_sympathy_rate": "0.78",
          "user_recent_delete_rate": "0.08"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "640",
          "nickname": "rpg1****",
          "user_nick": "rpg",
          "user_date": "2006-04-09",
          "user_history": "0.42",
          "user_total_rp": "946",
          "user_response": "682",
          "user_sympathy": "13,589",
          "user_recent_write": "131",
          "user_recent_delete": "20",
          "user_recent_sympathy": "4463",
          "user_recent_sympathy_rate": "0.68",
          "user_recent_delete_rate": "0.15"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "641",
          "nickname": "syeu****",
          "user_nick": "감사",
          "user_date": "2006-04-09",
          "user_history": "0.12",
          "user_total_rp": "334",
          "user_response": "3",
          "user_sympathy": "3,113",
          "user_recent_write": "10",
          "user_recent_delete": "0",
          "user_recent_sympathy": "20",
          "user_recent_sympathy_rate": "0.69",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "642",
          "nickname": "gydu****",
          "user_nick": "gyd",
          "user_date": "2006-04-09",
          "user_history": "0.34",
          "user_total_rp": "202",
          "user_response": "4",
          "user_sympathy": "799",
          "user_recent_write": "20",
          "user_recent_delete": "1",
          "user_recent_sympathy": "46",
          "user_recent_sympathy_rate": "0.92",
          "user_recent_delete_rate": "0.05"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "643",
          "nickname": "wind****",
          "user_nick": "Jiu",
          "user_date": "2006-04-09",
          "user_history": "0.16",
          "user_total_rp": "1,618",
          "user_response": "757",
          "user_sympathy": "13,311",
          "user_recent_write": "20",
          "user_recent_delete": "1",
          "user_recent_sympathy": "321",
          "user_recent_sympathy_rate": "0.89",
          "user_recent_delete_rate": "0.05"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "644",
          "nickname": "outl****",
          "user_nick": "기상청",
          "user_date": "2006-04-09",
          "user_history": "0.31",
          "user_total_rp": "521",
          "user_response": "141",
          "user_sympathy": "1,027",
          "user_recent_write": "14",
          "user_recent_delete": "1",
          "user_recent_sympathy": "20",
          "user_recent_sympathy_rate": "0.95",
          "user_recent_delete_rate": "0.07"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "645",
          "nickname": "fore****",
          "user_nick": "만식이엄마",
          "user_date": "2006-04-09",
          "user_history": "0.24",
          "user_total_rp": "2,533",
          "user_response": "221",
          "user_sympathy": "22,006",
          "user_recent_write": "220",
          "user_recent_delete": "8",
          "user_recent_sympathy": "765",
          "user_recent_sympathy_rate": "0.91",
          "user_recent_delete_rate": "0.04"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "646",
          "nickname": "taek****",
          "user_nick": "단무지",
          "user_date": "2006-04-09",
          "user_history": "0.38",
          "user_total_rp": "703",
          "user_response": "10",
          "user_sympathy": "1,958",
          "user_recent_write": "85",
          "user_recent_delete": "0",
          "user_recent_sympathy": "111",
          "user_recent_sympathy_rate": "0.73",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "647",
          "nickname": "jaso****",
          "user_nick": "왕대천사",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "22",
          "user_response": "1",
          "user_sympathy": "180",
          "user_recent_write": "14",
          "user_recent_delete": "0",
          "user_recent_sympathy": "137",
          "user_recent_sympathy_rate": "0.88",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "648",
          "nickname": "psm4****",
          "user_nick": "psm",
          "user_date": "2006-04-09",
          "user_history": "0.3",
          "user_total_rp": "654",
          "user_response": "960",
          "user_sympathy": "60,592",
          "user_recent_write": "0",
          "user_recent_delete": "0",
          "user_recent_sympathy": "0",
          "user_recent_sympathy_rate": "0.0",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "649",
          "nickname": "imcd****",
          "user_nick": "imc",
          "user_date": "2006-04-09",
          "user_history": "0.41",
          "user_total_rp": "118",
          "user_response": "179",
          "user_sympathy": "3,062",
          "user_recent_write": "3",
          "user_recent_delete": "0",
          "user_recent_sympathy": "3",
          "user_recent_sympathy_rate": "1.0",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "650",
          "nickname": "catd****",
          "user_nick": "하얀괭이",
          "user_date": "2006-04-09",
          "user_history": "0.34",
          "user_total_rp": "661",
          "user_response": "318",
          "user_sympathy": "10,026",
          "user_recent_write": "22",
          "user_recent_delete": "1",
          "user_recent_sympathy": "62",
          "user_recent_sympathy_rate": "0.65",
          "user_recent_delete_rate": "0.05"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "652",
          "nickname": "kkeg****",
          "user_nick": "콩꼬막",
          "user_date": "2006-04-09",
          "user_history": "0.38",
          "user_total_rp": "132",
          "user_response": "26",
          "user_sympathy": "561",
          "user_recent_write": "41",
          "user_recent_delete": "0",
          "user_recent_sympathy": "213",
          "user_recent_sympathy_rate": "0.96",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "653",
          "nickname": "300c****",
          "user_nick": "나야나",
          "user_date": "2006-04-09",
          "user_history": "0.29",
          "user_total_rp": "1,998",
          "user_response": "135",
          "user_sympathy": "23,952",
          "user_recent_write": "49",
          "user_recent_delete": "0",
          "user_recent_sympathy": "439",
          "user_recent_sympathy_rate": "0.89",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "654",
          "nickname": "chwh****",
          "user_nick": "jch89",
          "user_date": "2006-04-09",
          "user_history": "0.36",
          "user_total_rp": "367",
          "user_response": "17",
          "user_sympathy": "1,030",
          "user_recent_write": "60",
          "user_recent_delete": "12",
          "user_recent_sympathy": "239",
          "user_recent_sympathy_rate": "0.91",
          "user_recent_delete_rate": "0.2"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "655",
          "nickname": "sbbt****",
          "user_nick": "Travis",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "46",
          "user_response": "3",
          "user_sympathy": "192",
          "user_recent_write": "47",
          "user_recent_delete": "3",
          "user_recent_sympathy": "152",
          "user_recent_sympathy_rate": "0.81",
          "user_recent_delete_rate": "0.06"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "656",
          "nickname": "7icr****",
          "user_nick": "하로",
          "user_date": "2006-04-09",
          "user_history": "0.45",
          "user_total_rp": "126",
          "user_response": "79",
          "user_sympathy": "731",
          "user_recent_write": "29",
          "user_recent_delete": "0",
          "user_recent_sympathy": "26",
          "user_recent_sympathy_rate": "0.79",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "657",
          "nickname": "pice****",
          "user_nick": "레비앙",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "46",
          "user_response": "4",
          "user_sympathy": "381",
          "user_recent_write": "2",
          "user_recent_delete": "0",
          "user_recent_sympathy": "3",
          "user_recent_sympathy_rate": "1.0",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "658",
          "nickname": "rldb****",
          "user_nick": "rld",
          "user_date": "2006-04-09",
          "user_history": "0.21",
          "user_total_rp": "205",
          "user_response": "18",
          "user_sympathy": "1,727",
          "user_recent_write": "4",
          "user_recent_delete": "1",
          "user_recent_sympathy": "4",
          "user_recent_sympathy_rate": "0.67",
          "user_recent_delete_rate": "0.25"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "659",
          "nickname": "ss86****",
          "user_nick": "귀요미",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "38",
          "user_response": "9",
          "user_sympathy": "64",
          "user_recent_write": "7",
          "user_recent_delete": "0",
          "user_recent_sympathy": "6",
          "user_recent_sympathy_rate": "0.86",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "660",
          "nickname": "ttun****",
          "user_nick": "스카이워커",
          "user_date": "2006-04-09",
          "user_history": "0.33",
          "user_total_rp": "3,235",
          "user_response": "363",
          "user_sympathy": "11,240",
          "user_recent_write": "111",
          "user_recent_delete": "9",
          "user_recent_sympathy": "77",
          "user_recent_sympathy_rate": "0.5",
          "user_recent_delete_rate": "0.08"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "663",
          "nickname": "ceod****",
          "user_nick": "DODOceo",
          "user_date": "2006-04-09",
          "user_history": "0.34",
          "user_total_rp": "158",
          "user_response": "228",
          "user_sympathy": "429",
          "user_recent_write": "5",
          "user_recent_delete": "0",
          "user_recent_sympathy": "6",
          "user_recent_sympathy_rate": "0.86",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "664",
          "nickname": "ices****",
          "user_nick": "삐삐",
          "user_date": "2006-04-09",
          "user_history": "0.25",
          "user_total_rp": "205",
          "user_response": "78",
          "user_sympathy": "3,948",
          "user_recent_write": "12",
          "user_recent_delete": "0",
          "user_recent_sympathy": "41",
          "user_recent_sympathy_rate": "0.98",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "666",
          "nickname": "pjis****",
          "user_nick": "용감한 수호자",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "3",
          "user_response": "0",
          "user_sympathy": "5",
          "user_recent_write": "6",
          "user_recent_delete": "4",
          "user_recent_sympathy": "4",
          "user_recent_sympathy_rate": "1.0",
          "user_recent_delete_rate": "0.67"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "667",
          "nickname": "cj86****",
          "user_nick": "보스베이비",
          "user_date": "2006-04-09",
          "user_history": "0.32",
          "user_total_rp": "332",
          "user_response": "112",
          "user_sympathy": "1,343",
          "user_recent_write": "18",
          "user_recent_delete": "0",
          "user_recent_sympathy": "31",
          "user_recent_sympathy_rate": "0.57",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "668",
          "nickname": "mill****",
          "user_nick": "millenniumna",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "2",
          "user_response": "0",
          "user_sympathy": "3",
          "user_recent_write": "0",
          "user_recent_delete": "0",
          "user_recent_sympathy": "0",
          "user_recent_sympathy_rate": "0.0",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "669",
          "nickname": "smbe****",
          "user_nick": "초코아이스크림",
          "user_date": "2006-04-09",
          "user_history": "0.19",
          "user_total_rp": "784",
          "user_response": "195",
          "user_sympathy": "5,809",
          "user_recent_write": "33",
          "user_recent_delete": "1",
          "user_recent_sympathy": "165",
          "user_recent_sympathy_rate": "0.71",
          "user_recent_delete_rate": "0.03"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "670",
          "nickname": "jpop****",
          "user_nick": "Zzoo",
          "user_date": "2006-04-09",
          "user_history": "0.28",
          "user_total_rp": "1,870",
          "user_response": "375",
          "user_sympathy": "19,911",
          "user_recent_write": "270",
          "user_recent_delete": "10",
          "user_recent_sympathy": "897",
          "user_recent_sympathy_rate": "0.85",
          "user_recent_delete_rate": "0.04"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "671",
          "nickname": "tmtm****",
          "user_nick": "클리너디테일링",
          "user_date": "2006-04-09",
          "user_history": "0.3",
          "user_total_rp": "398",
          "user_response": "109",
          "user_sympathy": "26,975",
          "user_recent_write": "92",
          "user_recent_delete": "7",
          "user_recent_sympathy": "1599",
          "user_recent_sympathy_rate": "0.78",
          "user_recent_delete_rate": "0.08"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "672",
          "nickname": "chem****",
          "user_nick": "che",
          "user_date": "2006-04-09",
          "user_history": "0.38",
          "user_total_rp": "914",
          "user_response": "194",
          "user_sympathy": "7,628",
          "user_recent_write": "101",
          "user_recent_delete": "0",
          "user_recent_sympathy": "1896",
          "user_recent_sympathy_rate": "0.94",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "673",
          "nickname": "halb****",
          "user_nick": "Me",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "43",
          "user_response": "16",
          "user_sympathy": "528",
          "user_recent_write": "19",
          "user_recent_delete": "0",
          "user_recent_sympathy": "39",
          "user_recent_sympathy_rate": "0.93",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "675",
          "nickname": "jshy****",
          "user_nick": "노부농",
          "user_date": "2006-04-09",
          "user_history": "0.36",
          "user_total_rp": "749",
          "user_response": "77",
          "user_sympathy": "3,131",
          "user_recent_write": "122",
          "user_recent_delete": "0",
          "user_recent_sympathy": "176",
          "user_recent_sympathy_rate": "0.84",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "677",
          "nickname": "bgyn****",
          "user_nick": "Digil",
          "user_date": "2006-04-09",
          "user_history": "0.41",
          "user_total_rp": "2,089",
          "user_response": "76",
          "user_sympathy": "10,269",
          "user_recent_write": "223",
          "user_recent_delete": "20",
          "user_recent_sympathy": "967",
          "user_recent_sympathy_rate": "0.76",
          "user_recent_delete_rate": "0.09"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "679",
          "nickname": "ips4****",
          "user_nick": "ips",
          "user_date": "2006-04-09",
          "user_history": "0.28",
          "user_total_rp": "2,076",
          "user_response": "512",
          "user_sympathy": "15,134",
          "user_recent_write": "115",
          "user_recent_delete": "0",
          "user_recent_sympathy": "258",
          "user_recent_sympathy_rate": "0.79",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "680",
          "nickname": "woor****",
          "user_nick": "하루하루",
          "user_date": "2006-04-09",
          "user_history": "0.35",
          "user_total_rp": "2,278",
          "user_response": "480",
          "user_sympathy": "39,764",
          "user_recent_write": "137",
          "user_recent_delete": "0",
          "user_recent_sympathy": "1145",
          "user_recent_sympathy_rate": "0.93",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "682",
          "nickname": "bmwx****",
          "user_nick": "냉동학철학",
          "user_date": "2006-04-09",
          "user_history": "0.32",
          "user_total_rp": "177",
          "user_response": "1",
          "user_sympathy": "835",
          "user_recent_write": "142",
          "user_recent_delete": "5",
          "user_recent_sympathy": "422",
          "user_recent_sympathy_rate": "0.79",
          "user_recent_delete_rate": "0.04"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "683",
          "nickname": "shm1****",
          "user_nick": "sun",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "2",
          "user_response": "0",
          "user_sympathy": "1",
          "user_recent_write": "6",
          "user_recent_delete": "4",
          "user_recent_sympathy": "1",
          "user_recent_sympathy_rate": "1.0",
          "user_recent_delete_rate": "0.67"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "684",
          "nickname": "bbip****",
          "user_nick": "에비츄",
          "user_date": "2006-04-09",
          "user_history": "0.33",
          "user_total_rp": "278",
          "user_response": "218",
          "user_sympathy": "3,101",
          "user_recent_write": "9",
          "user_recent_delete": "0",
          "user_recent_sympathy": "7",
          "user_recent_sympathy_rate": "0.58",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "685",
          "nickname": "rlad****",
          "user_nick": "rladustn1201",
          "user_date": "2006-04-09",
          "user_history": "0.39",
          "user_total_rp": "2,998",
          "user_response": "208",
          "user_sympathy": "18,435",
          "user_recent_write": "154",
          "user_recent_delete": "1",
          "user_recent_sympathy": "1068",
          "user_recent_sympathy_rate": "0.89",
          "user_recent_delete_rate": "0.01"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "687",
          "nickname": "bnwo****",
          "user_nick": "진검",
          "user_date": "2006-04-09",
          "user_history": "0.29",
          "user_total_rp": "1,202",
          "user_response": "103",
          "user_sympathy": "15,350",
          "user_recent_write": "27",
          "user_recent_delete": "1",
          "user_recent_sympathy": "28",
          "user_recent_sympathy_rate": "0.8",
          "user_recent_delete_rate": "0.04"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "689",
          "nickname": "ceod****",
          "user_nick": "DODOceo",
          "user_date": "2006-04-09",
          "user_history": "0.34",
          "user_total_rp": "158",
          "user_response": "228",
          "user_sympathy": "429",
          "user_recent_write": "5",
          "user_recent_delete": "0",
          "user_recent_sympathy": "6",
          "user_recent_sympathy_rate": "0.86",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "690",
          "nickname": "pjm3****",
          "user_nick": "느어어어",
          "user_date": "2006-04-09",
          "user_history": "0.34",
          "user_total_rp": "340",
          "user_response": "125",
          "user_sympathy": "3,531",
          "user_recent_write": "26",
          "user_recent_delete": "10",
          "user_recent_sympathy": "699",
          "user_recent_sympathy_rate": "0.95",
          "user_recent_delete_rate": "0.38"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "692",
          "nickname": "youm****",
          "user_nick": "you",
          "user_date": "2006-04-09",
          "user_history": "0.22",
          "user_total_rp": "2,483",
          "user_response": "1,128",
          "user_sympathy": "24,011",
          "user_recent_write": "128",
          "user_recent_delete": "3",
          "user_recent_sympathy": "1376",
          "user_recent_sympathy_rate": "0.88",
          "user_recent_delete_rate": "0.02"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "693",
          "nickname": "punk****",
          "user_nick": "런던",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "69",
          "user_response": "28",
          "user_sympathy": "3,334",
          "user_recent_write": "0",
          "user_recent_delete": "0",
          "user_recent_sympathy": "0",
          "user_recent_sympathy_rate": "0.0",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "694",
          "nickname": "didr****",
          "user_nick": "did",
          "user_date": "2006-04-09",
          "user_history": "0.28",
          "user_total_rp": "746",
          "user_response": "225",
          "user_sympathy": "3,513",
          "user_recent_write": "181",
          "user_recent_delete": "0",
          "user_recent_sympathy": "641",
          "user_recent_sympathy_rate": "0.91",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "695",
          "nickname": "jrki****",
          "user_nick": "좋은사람",
          "user_date": "2006-04-09",
          "user_history": "0.4",
          "user_total_rp": "598",
          "user_response": "158",
          "user_sympathy": "3,502",
          "user_recent_write": "205",
          "user_recent_delete": "9",
          "user_recent_sympathy": "531",
          "user_recent_sympathy_rate": "0.87",
          "user_recent_delete_rate": "0.04"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "696",
          "nickname": "jj28****",
          "user_nick": "jj2",
          "user_date": "2006-04-09",
          "user_history": "0.26",
          "user_total_rp": "4,939",
          "user_response": "120",
          "user_sympathy": "55,826",
          "user_recent_write": "215",
          "user_recent_delete": "19",
          "user_recent_sympathy": "1213",
          "user_recent_sympathy_rate": "0.93",
          "user_recent_delete_rate": "0.09"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "697",
          "nickname": "crei****",
          "user_nick": "Tran",
          "user_date": "2006-04-09",
          "user_history": "0.23",
          "user_total_rp": "992",
          "user_response": "201",
          "user_sympathy": "9,323",
          "user_recent_write": "4",
          "user_recent_delete": "2",
          "user_recent_sympathy": "3",
          "user_recent_sympathy_rate": "0.5",
          "user_recent_delete_rate": "0.5"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "699",
          "nickname": "tlac****",
          "user_nick": "tlacogk",
          "user_date": "2006-04-09",
          "user_history": "0.32",
          "user_total_rp": "762",
          "user_response": "495",
          "user_sympathy": "6,749",
          "user_recent_write": "92",
          "user_recent_delete": "0",
          "user_recent_sympathy": "3864",
          "user_recent_sympathy_rate": "0.96",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "700",
          "nickname": "form****",
          "user_nick": "bo",
          "user_date": "2006-04-09",
          "user_history": "0.33",
          "user_total_rp": "208",
          "user_response": "36",
          "user_sympathy": "4,321",
          "user_recent_write": "3",
          "user_recent_delete": "0",
          "user_recent_sympathy": "94",
          "user_recent_sympathy_rate": "0.99",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "701",
          "nickname": "xodo****",
          "user_nick": "xod",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "4",
          "user_response": "1",
          "user_sympathy": "13",
          "user_recent_write": "2",
          "user_recent_delete": "0",
          "user_recent_sympathy": "0",
          "user_recent_sympathy_rate": "0.0",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "703",
          "nickname": "amur****",
          "user_nick": "amu",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "6",
          "user_response": "0",
          "user_sympathy": "21",
          "user_recent_write": "1",
          "user_recent_delete": "0",
          "user_recent_sympathy": "0",
          "user_recent_sympathy_rate": "0.0",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "704",
          "nickname": "noti****",
          "user_nick": "씀바귀",
          "user_date": "2006-04-09",
          "user_history": "0.51",
          "user_total_rp": "375",
          "user_response": "213",
          "user_sympathy": "723",
          "user_recent_write": "196",
          "user_recent_delete": "3",
          "user_recent_sympathy": "108",
          "user_recent_sympathy_rate": "0.38",
          "user_recent_delete_rate": "0.02"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "705",
          "nickname": "dmee****",
          "user_nick": "LYSLMS",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "67",
          "user_response": "10",
          "user_sympathy": "354",
          "user_recent_write": "35",
          "user_recent_delete": "0",
          "user_recent_sympathy": "170",
          "user_recent_sympathy_rate": "0.95",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "706",
          "nickname": "rin2****",
          "user_nick": "좋은하루",
          "user_date": "2006-04-09",
          "user_history": "0.31",
          "user_total_rp": "123",
          "user_response": "17",
          "user_sympathy": "6,593",
          "user_recent_write": "155",
          "user_recent_delete": "21",
          "user_recent_sympathy": "5857",
          "user_recent_sympathy_rate": "0.77",
          "user_recent_delete_rate": "0.14"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "707",
          "nickname": "kot7****",
          "user_nick": "kot",
          "user_date": "2006-04-09",
          "user_history": "0.4",
          "user_total_rp": "590",
          "user_response": "193",
          "user_sympathy": "1,656",
          "user_recent_write": "240",
          "user_recent_delete": "0",
          "user_recent_sympathy": "586",
          "user_recent_sympathy_rate": "0.65",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "708",
          "nickname": "zzan****",
          "user_nick": "지지아나",
          "user_date": "2006-04-09",
          "user_history": "0.35",
          "user_total_rp": "69",
          "user_response": "35",
          "user_sympathy": "1,897",
          "user_recent_write": "19",
          "user_recent_delete": "1",
          "user_recent_sympathy": "55",
          "user_recent_sympathy_rate": "0.77",
          "user_recent_delete_rate": "0.05"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "709",
          "nickname": "ssiw****",
          "user_nick": "슈다",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "35",
          "user_response": "1",
          "user_sympathy": "122",
          "user_recent_write": "1",
          "user_recent_delete": "0",
          "user_recent_sympathy": "0",
          "user_recent_sympathy_rate": "0.0",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "710",
          "nickname": "ices****",
          "user_nick": "삐삐",
          "user_date": "2006-04-09",
          "user_history": "0.25",
          "user_total_rp": "205",
          "user_response": "78",
          "user_sympathy": "3,948",
          "user_recent_write": "12",
          "user_recent_delete": "0",
          "user_recent_sympathy": "41",
          "user_recent_sympathy_rate": "0.98",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "711",
          "nickname": "chun****",
          "user_nick": "Sky Go",
          "user_date": "2006-04-09",
          "user_history": "0.47",
          "user_total_rp": "447",
          "user_response": "39",
          "user_sympathy": "559",
          "user_recent_write": "34",
          "user_recent_delete": "0",
          "user_recent_sympathy": "28",
          "user_recent_sympathy_rate": "0.72",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "713",
          "nickname": "sjb3****",
          "user_nick": "옹박",
          "user_date": "2006-04-09",
          "user_history": "0.3",
          "user_total_rp": "3,090",
          "user_response": "465",
          "user_sympathy": "20,898",
          "user_recent_write": "71",
          "user_recent_delete": "5",
          "user_recent_sympathy": "194",
          "user_recent_sympathy_rate": "0.78",
          "user_recent_delete_rate": "0.07"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "714",
          "nickname": "dkdl****",
          "user_nick": "쥬므란",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "71",
          "user_response": "23",
          "user_sympathy": "339",
          "user_recent_write": "14",
          "user_recent_delete": "0",
          "user_recent_sympathy": "9",
          "user_recent_sympathy_rate": "0.21",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "715",
          "nickname": "bamb****",
          "user_nick": "크르릉",
          "user_date": "2006-04-09",
          "user_history": "0.26",
          "user_total_rp": "1,456",
          "user_response": "271",
          "user_sympathy": "41,816",
          "user_recent_write": "19",
          "user_recent_delete": "1",
          "user_recent_sympathy": "99",
          "user_recent_sympathy_rate": "0.97",
          "user_recent_delete_rate": "0.05"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "716",
          "nickname": "kot7****",
          "user_nick": "kot",
          "user_date": "2006-04-09",
          "user_history": "0.4",
          "user_total_rp": "590",
          "user_response": "193",
          "user_sympathy": "1,656",
          "user_recent_write": "240",
          "user_recent_delete": "0",
          "user_recent_sympathy": "586",
          "user_recent_sympathy_rate": "0.65",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "717",
          "nickname": "smj1****",
          "user_nick": "haha",
          "user_date": "2006-04-09",
          "user_history": "0.44",
          "user_total_rp": "1,190",
          "user_response": "568",
          "user_sympathy": "19,031",
          "user_recent_write": "68",
          "user_recent_delete": "0",
          "user_recent_sympathy": "268",
          "user_recent_sympathy_rate": "0.86",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "718",
          "nickname": "kot7****",
          "user_nick": "kot",
          "user_date": "2006-04-09",
          "user_history": "0.4",
          "user_total_rp": "590",
          "user_response": "193",
          "user_sympathy": "1,656",
          "user_recent_write": "240",
          "user_recent_delete": "0",
          "user_recent_sympathy": "586",
          "user_recent_sympathy_rate": "0.65",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "720",
          "nickname": "fore****",
          "user_nick": "만식이엄마",
          "user_date": "2006-04-09",
          "user_history": "0.24",
          "user_total_rp": "2,533",
          "user_response": "221",
          "user_sympathy": "22,006",
          "user_recent_write": "220",
          "user_recent_delete": "8",
          "user_recent_sympathy": "765",
          "user_recent_sympathy_rate": "0.91",
          "user_recent_delete_rate": "0.04"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "721",
          "nickname": "jang****",
          "user_nick": "jan",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "1",
          "user_response": "0",
          "user_sympathy": "0",
          "user_recent_write": "1",
          "user_recent_delete": "0",
          "user_recent_sympathy": "0",
          "user_recent_sympathy_rate": "0.0",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "723",
          "nickname": "zxco****",
          "user_nick": "zxc",
          "user_date": "2006-04-09",
          "user_history": "0.26",
          "user_total_rp": "2,288",
          "user_response": "106",
          "user_sympathy": "32,174",
          "user_recent_write": "58",
          "user_recent_delete": "0",
          "user_recent_sympathy": "85",
          "user_recent_sympathy_rate": "0.57",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "725",
          "nickname": "shm1****",
          "user_nick": "sun",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "2",
          "user_response": "0",
          "user_sympathy": "1",
          "user_recent_write": "6",
          "user_recent_delete": "4",
          "user_recent_sympathy": "1",
          "user_recent_sympathy_rate": "1.0",
          "user_recent_delete_rate": "0.67"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "727",
          "nickname": "dlfn****",
          "user_nick": "dlf",
          "user_date": "2006-04-09",
          "user_history": "0.39",
          "user_total_rp": "54",
          "user_response": "72",
          "user_sympathy": "164",
          "user_recent_write": "17",
          "user_recent_delete": "1",
          "user_recent_sympathy": "29",
          "user_recent_sympathy_rate": "0.91",
          "user_recent_delete_rate": "0.06"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "728",
          "nickname": "kanv****",
          "user_nick": "kan",
          "user_date": "2006-04-09",
          "user_history": "0.34",
          "user_total_rp": "4,199",
          "user_response": "1,961",
          "user_sympathy": "41,565",
          "user_recent_write": "193",
          "user_recent_delete": "2",
          "user_recent_sympathy": "434",
          "user_recent_sympathy_rate": "0.55",
          "user_recent_delete_rate": "0.01"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "729",
          "nickname": "eunj****",
          "user_nick": "Alice Eunju Kim",
          "user_date": "2006-04-09",
          "user_history": "0.37",
          "user_total_rp": "178",
          "user_response": "43",
          "user_sympathy": "756",
          "user_recent_write": "41",
          "user_recent_delete": "7",
          "user_recent_sympathy": "101",
          "user_recent_sympathy_rate": "0.96",
          "user_recent_delete_rate": "0.17"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "730",
          "nickname": "hyea****",
          "user_nick": "MINE",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "65",
          "user_response": "4",
          "user_sympathy": "1,016",
          "user_recent_write": "6",
          "user_recent_delete": "0",
          "user_recent_sympathy": "1",
          "user_recent_sympathy_rate": "1.0",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "732",
          "nickname": "hell****",
          "user_nick": "hellopinky02",
          "user_date": "2006-04-09",
          "user_history": "0.49",
          "user_total_rp": "377",
          "user_response": "149",
          "user_sympathy": "5,048",
          "user_recent_write": "22",
          "user_recent_delete": "0",
          "user_recent_sympathy": "47",
          "user_recent_sympathy_rate": "0.78",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "733",
          "nickname": "trw2****",
          "user_nick": "준이",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "97",
          "user_response": "1",
          "user_sympathy": "109",
          "user_recent_write": "21",
          "user_recent_delete": "0",
          "user_recent_sympathy": "19",
          "user_recent_sympathy_rate": "0.51",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "734",
          "nickname": "qhrt****",
          "user_nick": "브레인",
          "user_date": "2006-04-09",
          "user_history": "0.32",
          "user_total_rp": "399",
          "user_response": "640",
          "user_sympathy": "5,847",
          "user_recent_write": "96",
          "user_recent_delete": "0",
          "user_recent_sympathy": "130",
          "user_recent_sympathy_rate": "0.74",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "735",
          "nickname": "hair****",
          "user_nick": "디자이너현민",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "5",
          "user_response": "3",
          "user_sympathy": "28",
          "user_recent_write": "1",
          "user_recent_delete": "0",
          "user_recent_sympathy": "0",
          "user_recent_sympathy_rate": "0.0",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "737",
          "nickname": "chan****",
          "user_nick": "최강젖히기",
          "user_date": "2006-04-09",
          "user_history": "0.35",
          "user_total_rp": "134",
          "user_response": "180",
          "user_sympathy": "968",
          "user_recent_write": "11",
          "user_recent_delete": "2",
          "user_recent_sympathy": "4",
          "user_recent_sympathy_rate": "0.57",
          "user_recent_delete_rate": "0.18"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "738",
          "nickname": "yous****",
          "user_nick": "츄츄",
          "user_date": "2006-04-09",
          "user_history": "0.25",
          "user_total_rp": "2,127",
          "user_response": "414",
          "user_sympathy": "26,471",
          "user_recent_write": "84",
          "user_recent_delete": "2",
          "user_recent_sympathy": "209",
          "user_recent_sympathy_rate": "0.54",
          "user_recent_delete_rate": "0.02"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "740",
          "nickname": "zzan****",
          "user_nick": "설현남편",
          "user_date": "2006-04-09",
          "user_history": "0.36",
          "user_total_rp": "187",
          "user_response": "42",
          "user_sympathy": "720",
          "user_recent_write": "1",
          "user_recent_delete": "0",
          "user_recent_sympathy": "0",
          "user_recent_sympathy_rate": "0.0",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "741",
          "nickname": "lhs0****",
          "user_nick": "lhs",
          "user_date": "2006-04-09",
          "user_history": "0.38",
          "user_total_rp": "360",
          "user_response": "82",
          "user_sympathy": "1,989",
          "user_recent_write": "11",
          "user_recent_delete": "1",
          "user_recent_sympathy": "21",
          "user_recent_sympathy_rate": "1.0",
          "user_recent_delete_rate": "0.09"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "743",
          "nickname": "sldr****",
          "user_nick": "sldrjaak",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "51",
          "user_response": "6",
          "user_sympathy": "233",
          "user_recent_write": "11",
          "user_recent_delete": "0",
          "user_recent_sympathy": "2",
          "user_recent_sympathy_rate": "0.33",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "744",
          "nickname": "endo****",
          "user_nick": "endo",
          "user_date": "2006-04-09",
          "user_history": "0.32",
          "user_total_rp": "674",
          "user_response": "44",
          "user_sympathy": "1,636",
          "user_recent_write": "56",
          "user_recent_delete": "0",
          "user_recent_sympathy": "620",
          "user_recent_sympathy_rate": "0.96",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "745",
          "nickname": "haro****",
          "user_nick": "제자리걸음",
          "user_date": "2006-04-09",
          "user_history": "0.35",
          "user_total_rp": "1,474",
          "user_response": "193",
          "user_sympathy": "57,220",
          "user_recent_write": "75",
          "user_recent_delete": "7",
          "user_recent_sympathy": "620",
          "user_recent_sympathy_rate": "0.93",
          "user_recent_delete_rate": "0.09"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "746",
          "nickname": "skam****",
          "user_nick": "ska",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "40",
          "user_response": "37",
          "user_sympathy": "526",
          "user_recent_write": "4",
          "user_recent_delete": "0",
          "user_recent_sympathy": "10",
          "user_recent_sympathy_rate": "1.0",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "747",
          "nickname": "lmw0****",
          "user_nick": "토끼풀잎",
          "user_date": "2006-04-09",
          "user_history": "0.54",
          "user_total_rp": "140",
          "user_response": "10",
          "user_sympathy": "977",
          "user_recent_write": "217",
          "user_recent_delete": "78",
          "user_recent_sympathy": "971",
          "user_recent_sympathy_rate": "0.89",
          "user_recent_delete_rate": "0.36"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "749",
          "nickname": "thes****",
          "user_nick": "템파",
          "user_date": "2006-04-09",
          "user_history": "0.28",
          "user_total_rp": "4,962",
          "user_response": "354",
          "user_sympathy": "21,050",
          "user_recent_write": "92",
          "user_recent_delete": "2",
          "user_recent_sympathy": "344",
          "user_recent_sympathy_rate": "0.69",
          "user_recent_delete_rate": "0.02"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "751",
          "nickname": "dlss****",
          "user_nick": "마음소리",
          "user_date": "2006-04-09",
          "user_history": "0.4",
          "user_total_rp": "160",
          "user_response": "17",
          "user_sympathy": "1,046",
          "user_recent_write": "56",
          "user_recent_delete": "1",
          "user_recent_sympathy": "259",
          "user_recent_sympathy_rate": "0.81",
          "user_recent_delete_rate": "0.02"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "754",
          "nickname": "seon****",
          "user_nick": "콩냥",
          "user_date": "2006-04-09",
          "user_history": "0.52",
          "user_total_rp": "2,756",
          "user_response": "1,048",
          "user_sympathy": "80,160",
          "user_recent_write": "161",
          "user_recent_delete": "0",
          "user_recent_sympathy": "579",
          "user_recent_sympathy_rate": "0.92",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "755",
          "nickname": "sdm1****",
          "user_nick": "sdm",
          "user_date": "2006-04-09",
          "user_history": "0.19",
          "user_total_rp": "1,058",
          "user_response": "115",
          "user_sympathy": "6,184",
          "user_recent_write": "10",
          "user_recent_delete": "0",
          "user_recent_sympathy": "13",
          "user_recent_sympathy_rate": "0.93",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "756",
          "nickname": "seah****",
          "user_nick": "sea",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "29",
          "user_response": "25",
          "user_sympathy": "197",
          "user_recent_write": "18",
          "user_recent_delete": "1",
          "user_recent_sympathy": "13",
          "user_recent_sympathy_rate": "0.81",
          "user_recent_delete_rate": "0.06"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "757",
          "nickname": "blue****",
          "user_nick": "블루드림",
          "user_date": "2006-04-09",
          "user_history": "0.37",
          "user_total_rp": "1,362",
          "user_response": "317",
          "user_sympathy": "17,728",
          "user_recent_write": "157",
          "user_recent_delete": "1",
          "user_recent_sympathy": "556",
          "user_recent_sympathy_rate": "0.85",
          "user_recent_delete_rate": "0.01"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "758",
          "nickname": "alsr****",
          "user_nick": "데이지킴",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "65",
          "user_response": "21",
          "user_sympathy": "376",
          "user_recent_write": "0",
          "user_recent_delete": "0",
          "user_recent_sympathy": "0",
          "user_recent_sympathy_rate": "0.0",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "759",
          "nickname": "bast****",
          "user_nick": "프로필",
          "user_date": "2006-04-09",
          "user_history": "0.44",
          "user_total_rp": "346",
          "user_response": "57",
          "user_sympathy": "16,343",
          "user_recent_write": "114",
          "user_recent_delete": "7",
          "user_recent_sympathy": "1639",
          "user_recent_sympathy_rate": "0.9",
          "user_recent_delete_rate": "0.06"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "760",
          "nickname": "kswo****",
          "user_nick": "워니",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "49",
          "user_response": "0",
          "user_sympathy": "153",
          "user_recent_write": "17",
          "user_recent_delete": "1",
          "user_recent_sympathy": "20",
          "user_recent_sympathy_rate": "0.83",
          "user_recent_delete_rate": "0.06"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "766",
          "nickname": "iamr****",
          "user_nick": "김희주",
          "user_date": "2006-04-09",
          "user_history": "0.33",
          "user_total_rp": "446",
          "user_response": "44",
          "user_sympathy": "10,630",
          "user_recent_write": "8",
          "user_recent_delete": "0",
          "user_recent_sympathy": "20",
          "user_recent_sympathy_rate": "0.59",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "767",
          "nickname": "runu****",
          "user_nick": "미니멀",
          "user_date": "2006-04-09",
          "user_history": "0.33",
          "user_total_rp": "2,473",
          "user_response": "1,244",
          "user_sympathy": "16,097",
          "user_recent_write": "64",
          "user_recent_delete": "7",
          "user_recent_sympathy": "328",
          "user_recent_sympathy_rate": "0.94",
          "user_recent_delete_rate": "0.11"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "768",
          "nickname": "seon****",
          "user_nick": "이정현",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "6",
          "user_response": "0",
          "user_sympathy": "15",
          "user_recent_write": "0",
          "user_recent_delete": "0",
          "user_recent_sympathy": "0",
          "user_recent_sympathy_rate": "0.0",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "769",
          "nickname": "0111****",
          "user_nick": "011",
          "user_date": "2006-04-09",
          "user_history": "0.39",
          "user_total_rp": "194",
          "user_response": "78",
          "user_sympathy": "4,166",
          "user_recent_write": "12",
          "user_recent_delete": "0",
          "user_recent_sympathy": "13",
          "user_recent_sympathy_rate": "1.0",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "770",
          "nickname": "fox3****",
          "user_nick": "fox3654",
          "user_date": "2006-04-09",
          "user_history": "0.34",
          "user_total_rp": "1,344",
          "user_response": "144",
          "user_sympathy": "10,249",
          "user_recent_write": "166",
          "user_recent_delete": "1",
          "user_recent_sympathy": "1760",
          "user_recent_sympathy_rate": "0.88",
          "user_recent_delete_rate": "0.01"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "771",
          "nickname": "jch3****",
          "user_nick": "jch3057681",
          "user_date": "2006-04-09",
          "user_history": "0.31",
          "user_total_rp": "5,841",
          "user_response": "372",
          "user_sympathy": "29,587",
          "user_recent_write": "211",
          "user_recent_delete": "1",
          "user_recent_sympathy": "246",
          "user_recent_sympathy_rate": "0.85",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "772",
          "nickname": "stea****",
          "user_nick": "카일리",
          "user_date": "2006-04-09",
          "user_history": "0.3",
          "user_total_rp": "738",
          "user_response": "5",
          "user_sympathy": "3,599",
          "user_recent_write": "46",
          "user_recent_delete": "16",
          "user_recent_sympathy": "152",
          "user_recent_sympathy_rate": "0.96",
          "user_recent_delete_rate": "0.35"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "773",
          "nickname": "leag****",
          "user_nick": "좋은세상만들기",
          "user_date": "2006-04-09",
          "user_history": "0.32",
          "user_total_rp": "241",
          "user_response": "52",
          "user_sympathy": "1,544",
          "user_recent_write": "0",
          "user_recent_delete": "0",
          "user_recent_sympathy": "0",
          "user_recent_sympathy_rate": "0.0",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "774",
          "nickname": "stai****",
          "user_nick": "sta",
          "user_date": "2006-04-09",
          "user_history": "0.27",
          "user_total_rp": "554",
          "user_response": "168",
          "user_sympathy": "17,758",
          "user_recent_write": "53",
          "user_recent_delete": "0",
          "user_recent_sympathy": "700",
          "user_recent_sympathy_rate": "0.94",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "776",
          "nickname": "kdss****",
          "user_nick": "와인",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "55",
          "user_response": "8",
          "user_sympathy": "7,705",
          "user_recent_write": "9",
          "user_recent_delete": "2",
          "user_recent_sympathy": "16",
          "user_recent_sympathy_rate": "0.48",
          "user_recent_delete_rate": "0.22"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "777",
          "nickname": "ssal****",
          "user_nick": "ssalbob",
          "user_date": "2006-04-09",
          "user_history": "0.29",
          "user_total_rp": "3,651",
          "user_response": "141",
          "user_sympathy": "55,285",
          "user_recent_write": "117",
          "user_recent_delete": "3",
          "user_recent_sympathy": "1514",
          "user_recent_sympathy_rate": "0.98",
          "user_recent_delete_rate": "0.03"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "778",
          "nickname": "fall****",
          "user_nick": "나의",
          "user_date": "2006-04-09",
          "user_history": "0.28",
          "user_total_rp": "9,991",
          "user_response": "1,064",
          "user_sympathy": "151,300",
          "user_recent_write": "163",
          "user_recent_delete": "3",
          "user_recent_sympathy": "1484",
          "user_recent_sympathy_rate": "0.83",
          "user_recent_delete_rate": "0.02"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "784",
          "nickname": "ocea****",
          "user_nick": "사냥꾼",
          "user_date": "2006-04-09",
          "user_history": "0.26",
          "user_total_rp": "912",
          "user_response": "62",
          "user_sympathy": "5,163",
          "user_recent_write": "30",
          "user_recent_delete": "0",
          "user_recent_sympathy": "57",
          "user_recent_sympathy_rate": "0.85",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "787",
          "nickname": "wind****",
          "user_nick": "Jiu",
          "user_date": "2006-04-09",
          "user_history": "0.16",
          "user_total_rp": "1,618",
          "user_response": "757",
          "user_sympathy": "13,311",
          "user_recent_write": "20",
          "user_recent_delete": "1",
          "user_recent_sympathy": "321",
          "user_recent_sympathy_rate": "0.89",
          "user_recent_delete_rate": "0.05"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "788",
          "nickname": "rose****",
          "user_nick": "Cranky Rosen",
          "user_date": "2006-04-09",
          "user_history": "0.35",
          "user_total_rp": "644",
          "user_response": "261",
          "user_sympathy": "3,952",
          "user_recent_write": "23",
          "user_recent_delete": "0",
          "user_recent_sympathy": "14",
          "user_recent_sympathy_rate": "0.67",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "789",
          "nickname": "qeen****",
          "user_nick": "S",
          "user_date": "2006-04-09",
          "user_history": "0.43",
          "user_total_rp": "2,060",
          "user_response": "715",
          "user_sympathy": "18,278",
          "user_recent_write": "37",
          "user_recent_delete": "0",
          "user_recent_sympathy": "70",
          "user_recent_sympathy_rate": "0.82",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "791",
          "nickname": "tlac****",
          "user_nick": "tlacogk",
          "user_date": "2006-04-09",
          "user_history": "0.32",
          "user_total_rp": "762",
          "user_response": "495",
          "user_sympathy": "6,749",
          "user_recent_write": "92",
          "user_recent_delete": "0",
          "user_recent_sympathy": "3864",
          "user_recent_sympathy_rate": "0.96",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "792",
          "nickname": "mgs0****",
          "user_nick": "mgs06049",
          "user_date": "2006-04-09",
          "user_history": "0.31",
          "user_total_rp": "176",
          "user_response": "46",
          "user_sympathy": "497",
          "user_recent_write": "54",
          "user_recent_delete": "2",
          "user_recent_sympathy": "10",
          "user_recent_sympathy_rate": "0.12",
          "user_recent_delete_rate": "0.04"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "793",
          "nickname": "touc****",
          "user_nick": "tou",
          "user_date": "2006-04-09",
          "user_history": "0.34",
          "user_total_rp": "1,282",
          "user_response": "298",
          "user_sympathy": "28,275",
          "user_recent_write": "34",
          "user_recent_delete": "0",
          "user_recent_sympathy": "83",
          "user_recent_sympathy_rate": "0.58",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "794",
          "nickname": "tkwk****",
          "user_nick": "tkw",
          "user_date": "2006-04-09",
          "user_history": "0.34",
          "user_total_rp": "76",
          "user_response": "82",
          "user_sympathy": "533",
          "user_recent_write": "102",
          "user_recent_delete": "3",
          "user_recent_sympathy": "134",
          "user_recent_sympathy_rate": "0.71",
          "user_recent_delete_rate": "0.03"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "795",
          "nickname": "kimc****",
          "user_nick": "kim",
          "user_date": "2006-04-09",
          "user_history": "0.5",
          "user_total_rp": "1",
          "user_response": "0",
          "user_sympathy": "0",
          "user_recent_write": "0",
          "user_recent_delete": "0",
          "user_recent_sympathy": "0",
          "user_recent_sympathy_rate": "0.0",
          "user_recent_delete_rate": "0.0"
        },
        {
          "naver_news_id": "4",
          "naver_news_comments_id": "799",
          "nickname": "kmhn****",
          "user_nick": "kmh",
          "user_date": "2006-04-09",
          "user_history": "0.37",
          "user_total_rp": "202",
          "user_response": "12",
          "user_sympathy": "280",
          "user_recent_write": "121",
          "user_recent_delete": "0",
          "user_recent_sympathy": "185",
          "user_recent_sympathy_rate": "0.54",
          "user_recent_delete_rate": "0.0"
        }
			],
			cur_comments_info_df: cur_comments_info_df,
      kgNode: kgNode,
      kgLink: kgLink,
      nodes: nodeNameList, 
      links: kgList,
      nodeSize:10,
      force : 500,
      canvas:false,
      offsetTop: 0,
      newsjj: newsjj,
      lineTest: lineTest,
      naverReply: naverReply,
      tab: null,
      counter: 0,
      items_title: [
        { tab: '기사1', content: 'T' },
        { tab: '기사2', content: 'Tab 2 Content' },
        { tab: '기사3', content: 'Tab 3 Content' },
        { tab: '기사4', content: 'Tab 4 Content' },
        { tab: '기사5', content: 'Tab 5 Content' }
      ],
      tab2: null,
      items2: [
        { tab2: '순공감순', content2: 'Tab 1 Content' },
        { tab2: '댓글순', content2: 'Tab 2 Content' },
        { tab2: '공감비율순', content2: 'Tab 3 Content' },
        { tab2: '감정별 분류', content2: 'Tab 4 Content' }
      ],
      tab3: null,
      items3: [
        { tab: '감정에 따른 댓글분포', content: 'Tab 1 Content' },
        { tab: 'ㅇㅇ에 따른 댓글분포', content: 'Tab 2 Content' }
      ],
      tab4: null,
      items4: [
        { tab: '이 기사의 댓글 분석', content: 'Tab 1 Content' },
        { tab: '유사 기사 포함 댓글 분석', content: 'Tab 2 Content' }
      ],
      test_tab: null,
      text: 'Lorem ipsum dolor sit amet..',
      all_items: [
        { theme: '주제1', article: '기사1' }
      ],
      selected: [2],
      // todoItems : [],
      // db_replies: [],
      like_order_list: [],
      reply_order_list: [],
      like_rate_order_list: [],
      sent_order_list: [],
      order_list: ['like_order_list','reply_order_list','like_rate_order_list','sent_order_list']
      // axios_list: [],
    }
  },
  created () {
    // this.axios_test();
    // this.setData()
    // this.dbLoad();
    this.like_order();
    this.reply_order();
    this.like_rate_order();
    this.sent_order();
    // this.getListAll();
    // this.getList();
  },
  mounted () {
    this.setZoom()
  },
  computed:{
    options(){
      return{
        force: this.force,
        size:{ w:600, h:600},
        nodeSize: this.nodeSize,
        nodeLabels: true,
        linkLabels: true,
        canvas: this.canvas,
        linkWidth:2
      }
    }
  },
  methods:{
    // getListAll : function () {
    //   this.$http.get('/api/data').then((response) => {
    //     this.todoItems = response.data.map(function (data) {
    //       return data;
    //     });
    //   });
    // },
    // axios_test: function(){
    //   axios.get('/')
    //     .then((response) =>{
    //       // this.axios_list = JSON.stringify(response.data);
    //       this.axios_list = JSON.stringify(response.data.map(function (data) {
    //         return data;
    //       }));  
    //     })
    // },
    // dbLoad: function() {
    //   axios.get('/api/data')
    //   .then((response)=>{
    //     this.db_replies = JSON.parse(JSON.stringify(response.data))
    //   })
    // },
    like_order: function() {
      axios.get('/api/data/like')
      .then((response)=>{
        this.like_order_list = JSON.parse(JSON.stringify(response.data))
      })
    },
    reply_order: function() {
      axios.get('/api/data/reply')
      .then((response)=>{
        this.reply_order_list = JSON.parse(JSON.stringify(response.data))
      })
    },
    like_rate_order: function() {
      axios.get('/api/data/like_rate')
      .then((response)=>{
        this.like_rate_order_list = JSON.parse(JSON.stringify(response.data))
      })
    },
    sent_order: function() {
      axios.get('/api/data/sent')
      .then((response)=>{
        this.sent_order_list = JSON.parse(JSON.stringify(response.data))
      })
    },
    // getList : function() {
    //   this.$http.get('/api/data').then((response) => {
    //     this.db_replies = response.data;
    //   })
    // },
    onScroll (e) {
      this.offsetTop = e.target.scrollTop
    },
    lcb (link) {
      return link
    },
    greet: function (event) {
      // 메소드 안에서 사용하는 `this` 는 Vue 인스턴스를 가리킵니다
      alert('Hello ' + this.name + '!')
      // const chartchart = this.$refs.gChart.chartObject;
      // this.$refs.gChart.chartObject.setSelection([{row:0,column:0}]);
      // gChart.setSelection(5,5) 
			// chartOptions.colors = ['red','#004411']
      // `event` 는 네이티브 DOM 이벤트입니다
      if (event) {
        alert(event.target.tagName)
      }
    },
    // selectHandler: function(event) {
    //   alert('A table row was selected');
    // },
    // setData () {
    //   const stratify = d3.stratify().id((d) => d.id).parentId((d) => d.parentId)
    //   const stratified = stratify(data)
    //   const tree = d3.tree().size([this.viewer.w, this.viewer.h])

    //   tree(stratified)
    //   this.nodes = stratified.descendants()
    //   this.lines = stratified.descendants().slice(1)
    // },
    // getDiagonal (d) {
    //   return `M${d.y},${d.x}C${d.parent.y + 100},${d.x} ${d.parent.y + 100},${d.parent.x} ${d.parent.y},${d.parent.x}`
    // },
    setZoom () {
      const zoom = d3.zoom().scaleExtent([1, 10]).on('zoom', this.onZoom)
      const selection = d3.select(this.$refs.svg)

      selection
        .call(zoom)
        .call(zoom.transform, this.initZoom())
    },
    initZoom () {
      this.zoom.x = 40
      this.zoom.y = 0
      this.zoom.k = 1

      return d3.zoomIdentity
        .translate(this.zoom.x, this.zoom.y)
        .scale(this.zoom.k)
    },
    onZoom () {
      this.zoom.x = d3.event.transform.x
      this.zoom.y = d3.event.transform.y
      this.zoom.k = d3.event.transform.k
    }
  },

}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=PT+Sans');
body{
  font-family: 'PT Sans', sans-serif;
  background-color: #eee;
}
.title{
  position:absolute;
  text-align: center;
  left: 2em;
}
h1,a{
  color: skyblue;
  text-decoration: none;
}

ul.menu {
  list-style: none;
  position: absolute;
  z-index: 100;
  min-width: 20em;
  text-align: left;
}
ul.menu li{
  margin-top: 1em;
  position: relative;
}

#m-end path, #m-start{
  fill: rgba(18, 120, 98, 0.8);
}
.node-label{
  font-size: 1.0em;
}
.link-label{
  fill: rgb(0, 69, 133);
  transform: translate(0,.5em);
  font-size: .8em;
  text-align: left;
}
ul.menu {
  list-style: none;
  position: absolute;
  z-index: 100;
  min-width: 20em;
  text-align: left;
}
ul.menu li{
  margin-top: 1em;
  position: relative;
}

</style>

