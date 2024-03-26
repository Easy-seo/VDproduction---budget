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
    <p>녹음/믹싱</p>
    <select v-model="sound">
      <option value="">선택하세요</option>
      <option v-for="(b, index) in sounds" :value="b" :key="'custom_' + index">{{ b }}</option>
    </select>
    <p>선택된 옵션: {{ sound }}</p>

    <p>총 구성 : {{ pd }} / {{ writer }} / {{ filming }} / {{ twoD }} / {{ threeD }} / {{ studioYes }} / {{ sound }}</p>

    &nbsp;
    &nbsp;
    <input type="number" id="priceInput" v-model="totalPrice">
    <button @click="savePriceFunction">저장</button>

    <!-- 저장된 가격 출력 -->
    <p v-if="savedPrice !== ''">클라이언트가 총 요청한 예산: {{ savePrice }}</p>


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
        <th class="tg-0pky"></th>
        <th class="tg-0pky"></th>
        <th class="tg-0pky"></th>
        <th class="tg-0pky"></th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td class="tg-0pky">메인작가, 보조작가</td>
        <td class="tg-0pky">{{ writerCost }}</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
      </tr>
      <tr>
        <td class="tg-0pky">촬영감독, 촬영보조</td>
        <td class="tg-0pky">{{ filmingCost }}</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
      </tr>
      <tr>
        <td class="tg-0pky">스튜디오</td>
        <td class="tg-0pky">{{ studioCost }}</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
      </tr>
      <tr>
        <td class="tg-0pky">추가 촬영기자재</td>
        <td class="tg-0pky">150,000</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
      </tr>
      <tr>
        <td class="tg-0pky">모델 섭외비</td>
        <td class="tg-0pky">250,000</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
      </tr>
      <tr>
        <td class="tg-0pky">2D 디자이너</td>
        <td class="tg-0pky">{{twoDCost}}</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
      </tr>
      <tr>
        <td class="tg-0pky">3D 디자이너</td>
        <td class="tg-0pky">{{threeDCost}}</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
      </tr>
      <tr>
        <td class="tg-0pky">편집시설비 (Rendering PC)</td>
        <td class="tg-0pky">{{ etc }}</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
      </tr>
      <tr>
        <td class="tg-0pky">녹음, 믹싱</td>
        <td class="tg-0pky">{{ soundCost }}</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
      </tr>
      <tr>
        <td class="tg-0pky">성우료</td>
        <td class="tg-0pky">200,000</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
      </tr>
      <tr>
        <td class="tg-0pky">저작권사용료</td>
        <td class="tg-0pky">100,000</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
      </tr>
      <tr>
        <td class="tg-0pky">CG비용</td>
        <td class="tg-0pky">100,000</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
      </tr>
      <tr>
        <td class="tg-0pky">번역</td>
        <td class="tg-0pky">{{ translationCost }}</td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
        <td class="tg-0pky"></td>
      </tr>
    </tbody>
    </table>




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
      writerCost : 100000,
      filmingCost : 200000,
      twoDCost: 150000,
      threeDCost: 150000,
      studioCost : 150000,
      etc : 20000,
      soundCost : 150000,
      translationCost : 200000,
      totalPrice:0,
      savePrice : 0
    };
  },
  methods: {
    savePriceFunction(){
      this.savePrice = this.totalPrice;
    }
  },
  watch:{
    studio(n){
      if(n === 'Yes'){
        this.studioYes = '스튜디오';
      }else{
        this.studioYes='';
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