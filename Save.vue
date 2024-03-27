<template>
  <div>
    <p>담당PD</p>
    <!-- <select v-model="pd">
      <option value="">선택하세요</option>
      <option v-for="(option, index) in pds" :value="option" :key="index">{{ option }}</option>
    </select> -->
    <p>선택된 옵션: {{ pd }}</p>
    
    &nbsp;
    <p>(현재 옵션을 선택하게 했지만 사실 버튼으로 해서 해당 사항만 들어가는지 안들어가는지 check하기만 하면 됨)</p>
    
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
    <button @click="addWeight">퍼센테이지 부여하기</button>
    <button @click="calculator">계산하기</button>

    <!-- 저장된 가격 출력 -->
    <p v-if="savedPrice !== ''">클라이언트가 총 요청한 예산: {{ totalPrice }} 만원</p>


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
        <th class="tg-0pky">담당 PD</th>
        <th class="tg-0pky">{{ pdCost }}</th>
        <th class="tg-0pky">{{ pdDay }}</th>
        <th class="tg-0pky"></th>
        <th class="tg-0pky">{{ pdTotal}}</th>
        <th class="tg-0pky">{{ pdNominal }}</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td class="tg-0pky">메인작가, 보조작가</td>
        <td class="tg-0pky">{{ writerCost }}</td>
        <td class="tg-0pky">{{ writerDay }}</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky">{{ writerTotal }}</td>
        <td class="tg-0pky">{{ writerNominal }}</td>
      </tr>
      <tr>
        <td class="tg-0pky">촬영감독, 촬영보조</td>
        <td class="tg-0pky">{{ filmingCost }}</td>
        <td class="tg-0pky">{{ filmingDay }}</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky">{{ filmingTotal }}</td>
        <td class="tg-0pky">{{ filmingNominal }}</td>
      </tr>
      <tr>
        <td class="tg-0pky">스튜디오</td>
        <td class="tg-0pky">{{ studioCost }}</td>
        <td class="tg-0pky">{{ studioDay }}</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky">{{ studioTotal }}</td>
        <td class="tg-0pky">{{ studioNominal }}</td>
      </tr>
      <tr>
        <td class="tg-0pky">추가 촬영기자재</td>
        <td class="tg-0pky">300,000</td>
        <td class="tg-0pky">0</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky">0</td>
        <td class="tg-0pky">0</td>
      </tr>
      <tr>
        <td class="tg-0pky">모델 섭외비</td>
        <td class="tg-0pky">250,000</td>
        <td class="tg-0pky">0</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky">0</td>
        <td class="tg-0pky">0</td>
      </tr>
      <tr>
        <td class="tg-0pky">2D 디자이너</td>
        <td class="tg-0pky">{{twoDCost}}</td>
        <td class="tg-0pky">{{ twoDDay }}</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky">{{ twoDTotal }}</td>
        <td class="tg-0pky">{{ twoDNominal }}</td>
      </tr>
      <tr>
        <td class="tg-0pky">3D 디자이너</td>
        <td class="tg-0pky">{{threeDCost}}</td>
        <td class="tg-0pky">{{ threeDDay }}</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky">{{ threeDTotal }}</td>
        <td class="tg-0pky">{{ threeDNominal }}</td>
      </tr>
      <tr>
        <td class="tg-0pky">편집시설비 (Rendering PC)</td>
        <td class="tg-0pky">{{ etcCost }}</td>
        <td class="tg-0pky">{{ etcDay }}</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky">{{ etcTotal }}</td>
        <td class="tg-0pky">{{ etcNominal }}</td>
      </tr>
      <tr>
        <td class="tg-0pky">녹음, 믹싱</td>
        <td class="tg-0pky">{{ soundCost }}</td>
        <td class="tg-0pky">{{ soundDay }}</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky">{{ soundTotal }}</td>
        <td class="tg-0pky">{{ soundNominal }}</td>
      </tr>
      <tr>
        <td class="tg-0pky">성우료</td>
        <td class="tg-0pky">200,000</td>
        <td class="tg-0pky">0</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky">0</td>
        <td class="tg-0pky">0</td>
      </tr>
      <tr>
        <td class="tg-0pky">저작권사용료</td>
        <td class="tg-0pky">100,000</td>
        <td class="tg-0pky">0</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky">0</td>
        <td class="tg-0pky">0</td>
      </tr>
      <tr>
        <td class="tg-0pky">CG비용</td>
        <td class="tg-0pky">200,000</td>
        <td class="tg-0pky">0</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky">0</td>
        <td class="tg-0pky">0</td>
      </tr>
      <tr>
        <td class="tg-0pky">번역</td>
        <td class="tg-0pky">{{ translationCost }}</td>
        <td class="tg-0pky">{{ translationDay }}</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky">{{ translationTotal }}</td>
        <td class="tg-0pky">{{ translationNominal }}</td>
      </tr>
    </tbody>
    </table>


  <span :style="{paddingLeft:'330px'}"> 총 합 : </span>
  <span :style="{paddingLeft:'20px'}">{{ (pdCost * pdDay + writerCost * writerDay + filmingCost * filmingDay + studioCost * studioDay + twoDCost * twoDDay + threeDCost *threeDDay + etcDay * etcCost + soundCost * soundDay + translationCost * translationDay)/10000 }} 만원</span>
  <span :style="{paddingLeft:'90px'}">{{ totalNominal/10000 }} 만원</span>

  </div>
</template>

<script>
export default {
  name : 'ShowPage',
  data() {
    return {
      pd: '담당 PD', // 선택한 옵션을 저장할 변수
      // pds: [  // 기본 옵션들의 목록
      //   '담당PD',
      // ],
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
        '디자인 기획',
        '소스편집',
        '컷 편집',
        '소스/모션 편집',
        '종합 편집',
        '모션 편집 타이틀',
        '컷/소스 편집',
        '기획',
        '컷/종합 편집',
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
      pdCost: 150000,
      writerCost : 200000,
      filmingCost : 200000,
      twoDCost: 150000,
      threeDCost: 300000,
      studioCost : 300000,
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

      // 각각이 가지는 퍼센테이지
      pdPer:0.15,
      writerPer:0.1,
      filmingPer:0.15,
      translationPer:0.1,
      twoDPer:0,
      threeDPer:0.4,
      soundPer:0.1,
      sum :0, //pd를 뺀 총 합 금액
      sumPer:0,

      // 명목비
      nominal : 0.4, //명목수익률
      pdTotal : 0, 
      writerTotal : 0, 
      filmingTotal : 0, 
      twoDTotal:0, 
      threeDTotal : 0, 
      studioTotal : 0, 
      etcTotal : 0,
      soundTotal : 0, 
      translationTotal : 0, 

      // 명목비로 쓸 새로운 항목
      pdNominal : 0,
      writerNominal : 0,
      filmingNominal :0,
      twoDNominal : 0,
      threeDNominal : 0,
      studioNominal : 0,
      etcNominal : 0,
      soundNominal : 0,
      translationNominal : 0,
      totalNominal : 0,
    };
  },
  methods: {
    savePriceFunction(){
      this.savePrice = Number(this.totalPrice) * 5000;
    },
    addWeight(){
      if(this.studioDay !== 0){
        this.savePrice -= this.studioCost; // 스튜디오 비용 추가
      }
      
      //
      if(this.translationYes != ''){
        this.sumPer += this.translationPer;
      }
      
      if(this.threeD != ''){
        this.sumPer += this.threeDPer;
      }
      if(this.writer != ''){
        this.sumPer += this.writerPer;
      }
      if(this.filming != ''){
        this.sumPer += this.filmingPer;
      }
      if(this.pd != ''){
        this.sumPer += this.pdPer;
      }
      if(this.sound != ''){
        this.sumPer += this.soundPer;
      }
      //console.log(1 - this.sumPer);
      // this.pdPer = this.percentage; 필요 없을 것 같음
      // 편집시설비는 밑에 계산에서 넣기
    },
    nominalFunction(totalNum){
      let roundNum = (totalNum/(1-this.nominal)).toFixed(4);
      return parseInt(roundNum);
    },
    calculator(){
      if(this.studioYes != ''){
          this.studioDay = 1;
          this.sum += this.studioCost;
          this.studioTotal = this.studioCost;
          this.studioNominal = this.nominalFunction(this.studioTotal);
          this.totalNominal += this.studioNominal;
        }
        
        if(this.translationYes != ''){
          this.translationDay = parseInt((this.savePrice*this.translationPer)/this.translationCost);
          this.translationTotal = this.translationCost * this.translationDay;
          this.sum += this.translationTotal;
          this.translationNominal = this.nominalFunction(this.translationTotal);
          this.totalNominal += this.translationNominal;
        }
        
        if(this.threeD != ''){
          this.threeDDay = parseInt((this.savePrice * this.threeDPer)/this.threeDCost);
          this.threeDTotal = this.threeDCost * this.threeDDay;
          this.sum += this.threeDTotal;
          this.threeDNominal = this.nominalFunction(this.threeDTotal);
          this.totalNominal += this.threeDNominal;
        }
        if(this.writer != ''){
          this.writerDay = parseInt((this.savePrice*this.writerPer)/this.writerCost);
          this.writerTotal = this.writerCost * this.writerDay;
          this.sum += this.writerTotal;
          this.writerNominal = this.nominalFunction(this.writerTotal);
          this.totalNominal += this.writerNominal;
        }
        if(this.filming != ''){
          this.filmingDay = parseInt((this.savePrice*this.filmingPer)/this.filmingCost);
          this.filmingTotal = this.filmingCost * this.filmingDay;
          this.sum += this.filmingTotal;
          this.filmingNominal = this.nominalFunction(this.filmingTotal);
          this.totalNominal += this.filmingNominal;
        }
        if(this.pd != ''){
          this.pdDay = parseInt((this.savePrice*this.pdPer)/this.pdCost);
          this.pdTotal = this.pdCost * this.pdDay;
          this.sum += this.pdTotal;
          this.pdNominal = this.nominalFunction(this.pdTotal);
          this.totalNominal += this.pdNominal;
          console.log(this.pdDay);
        }
        if(this.sound != ''){
          this.soundDay = parseInt((this.savePrice*this.soundPer)/this.soundCost);
          this.soundTotal = this.soundCost * this.soundDay;
          this.sum += this.soundTotal;
          this.soundNominal = this.nominalFunction(this.soundTotal);
          this.totalNominal += this.soundNominal;
        }
        this.twoDDay = parseInt((this.savePrice - this.sum) / this.twoDCost);
        this.twoDTotal = this.twoDDay * this.twoDCost;
        this.sum += this.twoDTotal;
        this.twoDNominal = this.nominalFunction(this.twoDTotal);
        this.totalNominal += this.twoDNominal;
        
        this.etcDay = parseInt((this.savePrice - this.sum) / this.etcCost);
        this.etcTotal = this.etcCost * this.etcDay;
        this.etcNominal = this.nominalFunction(this.etcTotal);
        this.totalNominal += this.etcNominal;

        // 편집시설비가 너무 많이 들어가면
        if(this.etcDay > 5){
          // 너무 과하게 들어간 편집시설비, 
          let a = this.etcDay - 5; // 12면 12-5 = 7 그러면
          let b = a * this.etcCost; // 넘친 날만큼 다시 비용으로 만들기
          this.pdDay = parseInt(b/this.pdCost); // 넘친 비용을 pd에게 몰기
          this.etcDay -= this.pdDay;

          this.pdTotal = this.pdCost * this.pdDay;
          this.sum += this.pdTotal;
          this.pdNominal = this.nominalFunction(this.pdTotal);
          this.totalNominal += this.pdNominal;

          this.etcTotal = this.etcCost * this.etcDay;
          this.etcNominal = this.nominalFunction(this.etcTotal);
          this.totalNominal += this.etcNominal;
        }
      },

  },
  watch:{
    studio(n){
      if(n === 'Yes'){
        this.studioYes = '스튜디오';
        this.studioDay = 1;
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
div{
  padding: 20px;
}
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
