<template>
    <div>
      <p>담당PD</p>
      <select v-model="pd">
        <option value="">선택하세요</option>
        <option v-for="(option, index) in pds" :value="option" :key="index">{{ option }}</option>
      </select>
      <p>선택된 옵션: {{ pd }}</p>
      
      &nbsp;
      
      <p>메인작가/보조작가</p>
      <select v-model="writer">
        <option value="">선택하세요</option>
        <option v-for="(a, index) in writers" :value="a" :key="'custom_' + index">{{ a }}</option>
      </select>
      <p>선택된 옵션: {{ writer }}</p>
      
      &nbsp;
      
      <p>촬영감독</p>
      <select v-model="filming">
        <option value="">선택하세요</option>
        <option v-for="(b, index) in filmings" :value="b" :key="'custom_' + index">{{ b }}</option>
      </select>
      <p>선택된 옵션: {{ filming }}</p>
      
      &nbsp;
      
      <p>2D</p>
      <select v-model="twoD">
        <option value="">선택하세요</option>
        <option v-for="(b, index) in twoDs" :value="b" :key="'custom_' + index">{{ b }}</option>
      </select>
      <p>선택된 옵션: {{ twoD }}</p>
      
      &nbsp;
      
      <p>3D</p>
      <select v-model="threeD">
        <option value="">선택하세요</option>
        <option v-for="(b, index) in threeDs" :value="b" :key="'custom_' + index">{{ b }}</option>
      </select>
      <p>선택된 옵션: {{ threeD }}</p>
      
      &nbsp;
      <p>스튜디오</p>
      <select v-model="studio">
        <option value="">선택하세요</option>
        <option value="Yes">Yes</option>
      </select>
      <p v-if="studio !== ''">선택된 옵션: {{ studioYes }}</p>
      <p v-else>옵션을 선택하세요</p>
  
      &nbsp;
      <p>번역</p>
      <select v-model="translation">
        <option value="">선택하세요</option>
        <option value="Yes">Yes</option>
      </select>
      <p v-if="translation !== ''">선택된 옵션: {{ translationYes }}</p>
      <p v-else>옵션을 선택하세요</p>
      
      &nbsp;
      <p>녹음/믹싱</p>
      <select v-model="sound">
        <option value="">선택하세요</option>
        <option v-for="(b, index) in sounds" :value="b" :key="'custom_' + index">{{ b }}</option>
      </select>
      <p>선택된 옵션: {{ sound }}</p>
  
      <p>총 구성 : {{ pd }} / {{ writer }} / {{ filming }} / {{ twoD }} / {{ threeD }} / {{ studioYes }}/ {{ translationYes }} / {{ sound }}</p>
  
      &nbsp;
      &nbsp;
      <input type="number" id="priceInput" v-model="totalPrice">
      <button @click="savePriceFunction">저장</button>
      <button @click="calculator">계산하기</button>
  
      <!-- 저장된 가격 출력 -->
      <p v-if="savedPrice !== ''">클라이언트가 총 요청한 예산: {{ totalPrice*10000 }}</p>
  
  
      <table class="tg">
      <colgroup>
      <col style="width: 139px">
      <col style="width: 100px">
      <col style="width: 58px">
      <col style="width: 87px">
      <col style="width: 105px">
      <col style="width: 132px">
      </colgroup>
      <thead>
        <tr>
          <th class="tg-0pky">담당PD</th>
          <th class="tg-0pky">{{ pdCost }}</th>
          <th class="tg-0pky">{{ pdDay }}</th>
          <th class="tg-0pky"></th>
          <th class="tg-0pky">{{ pdCost * pdDay }}</th>
          <th class="tg-0pky"></th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td class="tg-0pky">메인작가, 보조작가</td>
          <td class="tg-0pky">{{ writerCost }}</td>
          <td class="tg-0pky">{{ writerDay }}</td>
          <td class="tg-0pky"></td>
          <td class="tg-0pky">{{ writerCost * writerDay }}</td>
          <td class="tg-0pky"></td>
        </tr>
        <tr>
          <td class="tg-0pky">촬영감독, 촬영보조</td>
          <td class="tg-0pky">{{ filmingCost }}</td>
          <td class="tg-0pky">{{ filmingDay }}</td>
          <td class="tg-0pky"></td>
          <td class="tg-0pky">{{ filmingCost * filmingDay }}</td>
          <td class="tg-0pky"></td>
        </tr>
        <tr>
          <td class="tg-0pky">스튜디오</td>
          <td class="tg-0pky">{{ studioCost }}</td>
          <td class="tg-0pky">{{ studioDay }}</td>
          <td class="tg-0pky"></td>
          <td class="tg-0pky">{{ studioCost * studioDay }}</td>
          <td class="tg-0pky"></td>
        </tr>
        <tr>
          <td class="tg-0pky">추가 촬영기자재</td>
          <td class="tg-0pky">150,000</td>
          <td class="tg-0pky">0</td>
          <td class="tg-0pky"></td>
          <td class="tg-0pky">0</td>
          <td class="tg-0pky"></td>
        </tr>
        <tr>
          <td class="tg-0pky">모델 섭외비</td>
          <td class="tg-0pky">250,000</td>
          <td class="tg-0pky">0</td>
          <td class="tg-0pky"></td>
          <td class="tg-0pky">0</td>
          <td class="tg-0pky"></td>
        </tr>
        <tr>
          <td class="tg-0pky">2D 디자이너</td>
          <td class="tg-0pky">{{twoDCost}}</td>
          <td class="tg-0pky">{{ twoDDay }}</td>
          <td class="tg-0pky"></td>
          <td class="tg-0pky">{{ twoDCost * twoDDay }}</td>
          <td class="tg-0pky"></td>
        </tr>
        <tr>
          <td class="tg-0pky">3D 디자이너</td>
          <td class="tg-0pky">{{threeDCost}}</td>
          <td class="tg-0pky">{{ threeDDay }}</td>
          <td class="tg-0pky"></td>
          <td class="tg-0pky">{{ threeDCost *threeDDay }}</td>
          <td class="tg-0pky"></td>
        </tr>
        <tr>
          <td class="tg-0pky">편집시설비 (Rendering PC)</td>
          <td class="tg-0pky">{{ etcCost }}</td>
          <td class="tg-0pky">{{ etcDay }}</td>
          <td class="tg-0pky"></td>
          <td class="tg-0pky">{{ etcDay * etcCost }}</td>
          <td class="tg-0pky"></td>
        </tr>
        <tr>
          <td class="tg-0pky">녹음, 믹싱</td>
          <td class="tg-0pky">{{ soundCost }}</td>
          <td class="tg-0pky">{{ soundDay }}</td>
          <td class="tg-0pky"></td>
          <td class="tg-0pky">{{ soundCost * soundDay }}</td>
          <td class="tg-0pky"></td>
        </tr>
        <tr>
          <td class="tg-0pky">성우료</td>
          <td class="tg-0pky">200,000</td>
          <td class="tg-0pky">0</td>
          <td class="tg-0pky"></td>
          <td class="tg-0pky">0</td>
          <td class="tg-0pky"></td>
        </tr>
        <tr>
          <td class="tg-0pky">저작권사용료</td>
          <td class="tg-0pky">100,000</td>
          <td class="tg-0pky">0</td>
          <td class="tg-0pky"></td>
          <td class="tg-0pky">0</td>
          <td class="tg-0pky"></td>
        </tr>
        <tr>
          <td class="tg-0pky">CG비용</td>
          <td class="tg-0pky">100,000</td>
          <td class="tg-0pky">0</td>
          <td class="tg-0pky"></td>
          <td class="tg-0pky">0</td>
          <td class="tg-0pky"></td>
        </tr>
        <tr>
          <td class="tg-0pky">번역</td>
          <td class="tg-0pky">{{ translationCost }}</td>
          <td class="tg-0pky">{{ translationDay }}</td>
          <td class="tg-0pky"></td>
          <td class="tg-0pky">{{ translationCost * translationDay }}</td>
          <td class="tg-0pky"></td>
        </tr>
      </tbody>
      </table>
  
  
    <span :style="{paddingLeft:'350px'}"> 총 합 : </span>
    <span :style="{paddingLeft:'33px'}">{{ pdCost * pdDay + writerCost * writerDay + filmingCost * filmingDay + studioCost * studioDay + twoDCost * twoDDay + threeDCost *threeDDay + etcDay * etcCost + soundCost * soundDay + translationCost * translationDay }}</span>
  
  
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        pd: '', // 선택한 옵션을 저장할 변수
        pds: [  // 기본 옵션들의 목록
          '소스편집',
          '컷 편집',
          '소스/모션 편집',
          '종합 편집',
          '모션 편집 타이틀',
          '컷/소스 편집',
          '기획',
          '컷/종합 편집'
        ],
        writer:'',
        writers: [  // 추가적인 옵션들의 목록
          '구성',
          '디자인 기획',
          '구성 스토리보드'
        ],
        filming:'',
        filmings: [  // 추가적인 옵션들의 목록
          '촬영',
          '촬영/조명',
          '행사 촬영 (1캠)',
          '행사 촬영 (2캠)',
          '전자칠판 촬영 (1일)',
          '전자칠판 촬영',
          '촬영 중계 (1캠)',
          '촬영 중계 (2캠)',
          '촬영 중계 (3캠)',
          '스튜디오 촬영',
          '씨네 촬영/색보정',
          '씨네/드론 촬영/색보정',
          '스탠다드/드론 촬영',
          '씨네 촬영/색보정',
          '실사촬영 (1회차)',
          '구성',
          '디자인 기획',
          '구성 스토리보드'
        ],
        twoD:'',
        twoDs:[
          '기본 타이포그래피',
          '기본 타이포그래피 타이틀',
          '인포그래픽',
          '색상 베리에이션(3종)',
          '턴어라운드 이미지',
          '타이포그래피 타이틀',
          '인포그래픽',
          '인포/모션그래픽',
          '인포/모션그래픽(고밀도)',
          '기존 영상 인트로/아웃트로 활용/모션 편집',
          '2D 모션 그래픽 (저밀도)',
          '2D 모션그래픽(중밀도)',
          '모션 편집 타이틀',
          '모션 편집',
          '인포 편집',
          '모션 편집/그래픽',
          '시퀀스 디자인',
          '인포/모션그래픽(고밀도)/2.5D',
          '3분 내외 2D 모션그래픽 편집',
          '2D일러스트 모션그래픽 편집',
          '모델링 파일',
          '디자인 기획'
        ],
        threeD:'',
        threeDs:[
          '2.5D',
          '인포/모션그래픽(고밀도)/2.5',
          'low density 3D 모델링/렌더링',
          'middle density 3D 모델링/렌더링',
          'middle density 3D 모델링/맵핑/렌더링',
          'high density 3D 모델링/맵핑/렌더링',
          '3분 내외 3D 모션그래픽 편집',
          '모션 편집/모션그래픽/3D'
        ],
        studio :'',
        studioYes:'',
        translation:'',
        translationYes:'',
        sound:'',
        sounds:[
          '사운드',
          '믹싱/국문 성우',
          '동시녹음',
          'TTS사운드진행',
          '사운드/국문 성우',
          '사운드믹싱',
        ],
        sum : 0,
        pdCost: 150000,
        writerCost : 100000,
        filmingCost : 200000,
        twoDCost: 150000,
        threeDCost: 150000,
        studioCost : 150000,
        etcCost : 20000,
        soundCost : 150000,
        translationCost : 200000,
        totalPrice:0, //사용자가 입력한 예산 금액
        savePrice : 0, // 원본 총 예산 금액
        pdDay : 0,
        writerDay : 0,
        filmingDay:0,
        studioDay : 0,
        translationDay : 0,
        twoDDay : 0,
        threeDDay : 0,
        soundDay : 0,
        etcDay : 0,
        remain : 0,
      };
    },
    methods: {
      savePriceFunction(){
        this.savePrice = Number(this.totalPrice) * 10000;
      },
      calculator(){
        if(this.studioYes != ''){
          this.studioDay = 1;
          this.sum += this.studioCost;
          this.savePrice -= this.studioCost;
        }
        if(this.translationYes != ''){
          this.translationDay = parseInt((this.savePrice*0.1)/this.translationCost);
          this.savePrice -= (this.translationDay * this.translationCost);
          this.sum += (this.translationDay * this.translationCost);
        }
  
        if(this.threeD != ''){
          this.threeDDay = parseInt((this.savePrice * 0.17)/this.threeDCost);
          this.savePrice -= (this.threeDDay * this.threeDCost);
          this.sum += (this.threeDDay * this.threeDCost);
        }
        if (this.writer != ''){
          this.writerDay = parseInt((this.savePrice*0.05)/this.writerCost);
          this.savePrice -= (this.writerDay*this.writerCost);
          this.sum += this.writerDay*this.writerCost;
          console.log(this.savePrice);
        }
        if(this.filming != ''){
          this.filmingDay = parseInt((this.savePrice*0.23)/this.filmingCost);
          this.savePrice -= (this.filmingCost * this.filmingDay);
          this.sum += (this.filmingCost * this.filmingDay);
        }
        if (this.twoD != ''){
          this.twoDDay = parseInt((this.savePrice*0.43)/this.twoDCost);
          this.savePrice -= (this.twoDCost * this.twoDDay);
          this.sum += (this.twoDCost * this.twoDDay);
        }
        if(this.sound != ''){
          this.soundDay = parseInt((this.savePrice*0.2)/this.soundCost);
          this.savePrice -= (this.soundCost * this.soundDay);
          this.sum += (this.soundCost * this.soundDay);
        }
        
        if (this.pd != ''){
          this.remain = this.totalPrice - this.sum;
          console.log(this.remain);
          this.pdDay = parseInt(this.remain / this.pdCost);
          this.remain -= this.pdDay * this.pdCost;  
        }
  
        if(this.remain > 0){
          this.etcDay = parseInt(this.remain / this.etcCost);
        }
  
        
      }
    },
    watch:{
      studio(n){
        if(n === 'Yes'){
          this.studioYes = '스튜디오';
        }else{
          this.studioYes='';
        }
      },
      translation(n){
        if(n === 'Yes'){
          this.translationYes = '번역';
        }else{
          this.translationYes='';
        }
      }
    }
  };
  </script>
  <style>
  .tg  {border-collapse:collapse;border-spacing:0;}
  .tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
    overflow:hidden;padding:10px 5px;word-break:normal;}
  .tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
    font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
  .tg .tg-0pky{border-color:inherit;text-align:left;vertical-align:top}
  .tg {
    width: 621px;
    table-layout: fixed;
  }
  
  .tg th, .tg td {
    border: 1px solid #000;
    padding: 10px;
    text-align: center;
  }
  
  </style>