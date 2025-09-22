---
layout: center
highlighter: shiki
css: unocss
colorSchema: dark
transition: fade-out
title: Secure Extract PII with LangExtract & Ollama
exportFilename: Extract PII PoC - Secure PII Extraction with Local LLM
lineNumbers: false
drawings:
  persist: false
mdc: true
clicks: 0
preload: false
glowSeed: 229
routerMode: hash
---

<div translate-x--14>

<h1>
  Secure Extract PII<br>
  <span class="text-blue-400">with LangExtract & Ollama</span>
</h1>

<div class="mt-8 text-xl opacity-80">
  로컬 LLM을 활용한 안전한 개인식별정보 추출
</div>

</div>

<div w-full absolute bottom-0 left-0 flex items-center transform="translate-x--10 translate-y--10">
  <div w-full flex items-center justify-end gap-4>
    <div class="text-sm opacity-60">2025.09.19</div>
  </div>
</div>

---
layout: intro
class: px-24
glowSeed: 205
---

<div flex items-center justify-center>
  <div
    class="border-2 border-white/20 rounded-xl p-8 bg-white/5 backdrop-blur-sm"
    w-fit
  >
    <div class="text-6xl mb-4 text-center">🔒</div>
    <div class="text-2xl mb-2 text-blue-300">Secure PII Extraction</div>
    <div class="text-lg opacity-80 text-center max-w-80">
      외부 서비스에 보내기 민감한<br>
      개인식별정보를 로컬에서<br>
      안전하게 추출하는 방법
    </div>
  </div>
</div>

---
layout: intro
class: px-35
glowSeed: 205
---

<div flex items-center justify-center>
  <div
    v-click flex flex-col items-center transition duration-500 ease-in-out
    :class="$clicks < 1 ? 'translate-y-20 opacity-0' : 'translate-y-0 opacity-100'"
  >
    <img src="/profile.jpg" w-50 h-50 rounded-full object-cover mb-5>
    <span font-semibold text-3xl>장진수</span>
    <div items-center>
      <div>
        <div class="opacity-70 text-center">신제품개발팀 팀장</div>
      </div>
      <div text-sm flex items-center justify-center gap-2 mt-4>
        <div i-ri:github-fill /><span underline decoration-dashed font-mono decoration-zinc-300>huketo</span>
      </div>
      <div text-sm flex items-center justify-center gap-2 mt-2>
        <div class="text-yellow-400">⭐</div>
        <span class="opacity-70 italic">"할일을 다하고, 천명을 기다려라"</span>
      </div>
    </div>
  </div>
</div>

---
layout: center
class: text-center
---

# 문제 상황: "건초더미에서 바늘 찾기"

<div class="mt-8">
  <div class="text-xl opacity-80">
    방대한 비정형 텍스트 속에서 PII를 안전하게 추출해야 한다면?
  </div>
</div>

<div class="mt-8 grid grid-cols-3 gap-4">

<v-click>
<div class="bg-red-900/20 border border-red-800/50 rounded-lg p-4">
  <div class="text-4xl mb-2">⚠️</div>
  <div class="text-lg font-bold text-red-300 mb-2">외부 서비스 의존</div>
  <div class="text-sm opacity-80">민감한 PII를<br>클라우드 API로 전송</div>
</div>
</v-click>

<v-click>
<div class="bg-yellow-900/20 border border-yellow-800/50 rounded-lg p-4">
  <div class="text-4xl mb-2">🔧</div>
  <div class="text-lg font-bold text-yellow-300 mb-2">복잡한 규칙 관리</div>
  <div class="text-sm opacity-80">정규식과 규칙 기반<br>시스템의 한계</div>
</div>
</v-click>

<v-click>
<div class="bg-purple-900/20 border border-purple-800/50 rounded-lg p-4">
  <div class="text-4xl mb-2">⏱️</div>
  <div class="text-lg font-bold text-purple-300 mb-2">긴 개발 사이클</div>
  <div class="text-sm opacity-80">모델 훈련과<br>파인튜닝의 부담</div>
</div>
</v-click>

</div>

---
class: py-10
glowSeed: 100
---

# 데이터 추출 기술의 진화

<span>From regex to LLM</span>

<div mt-6 />

<div grid grid-cols-3 gap-4 h-75>

<v-clicks>

<div border="2 solid white/10" rounded-lg overflow-hidden bg="white/5" backdrop-blur-sm h-full>
  <div flex items-center bg="red-900/30" px-4 py-3 rounded-t>
    <div i-carbon:code text-2xl mr-2 />
    <span font-bold>1. 정규 표현식</span>
  </div>
  <div p-4>
    <img src="/regex.png" alt="Regular Expression" class="w-full h-32 object-cover rounded mb-3">
    <div class="text-sm space-y-2">
      <div class="text-green-400">✓ 특정 패턴에 효과적</div>
      <div class="text-red-400">✗ 유지보수 어려움</div>
      <div class="text-red-400">✗ 새로운 PII 유형 한계</div>
    </div>
  </div>
</div>

<div border="2 solid white/10" rounded-lg overflow-hidden bg="white/5" backdrop-blur-sm h-full>
  <div flex items-center bg="blue-900/30" px-4 py-3 rounded-t>
    <div i-carbon:machine-learning-model text-2xl mr-2 />
    <span font-bold>2. 머신러닝 (BERT)</span>
  </div>
  <div p-4>
    <img src="/bert.png" alt="BERT Model" class="w-full h-32 object-cover rounded mb-3">
    <div class="text-sm space-y-2">
      <div class="text-green-400">✓ 컨텍스트 이해 향상</div>
      <div class="text-green-400">✓ 512 토큰 컨텍스트</div>
      <div class="text-red-400">✗ 대규모 라벨링 필요</div>
    </div>
  </div>
</div>

<div border="2 solid white/10" rounded-lg overflow-hidden bg="white/5" backdrop-blur-sm h-full>
  <div flex items-center bg="green-900/30" px-4 py-3 rounded-t>
    <div i-carbon:ibm-watson-language-translator text-2xl mr-2 />
    <span font-bold>3. LLM (GPT/Gemma)</span>
  </div>
  <div p-4>
    <img src="/encoder-decoder.png" alt="Transformer Model" class="w-full h-32 object-cover rounded mb-3">
    <div class="text-sm space-y-2">
      <div class="text-green-400">✓ 프롬프트 엔지니어링</div>
      <div class="text-green-400">✓ 긴 컨텍스트 처리</div>
      <div class="text-green-400">✓ 라벨링 부담 감소</div>
    </div>
  </div>
</div>

</v-clicks>

</div>

---
class: py-10
glowSeed: 175
---

<div flex justify-between items-start>
  <div>
    <h1>LangExtract의 등장</h1>
    <div>LLM 기반 정보 추출의 새로운 표준</div>
  </div>
  <img src="/langextract-hero.png" alt="LangExtract" class="h-48 rounded-lg shadow-2xl">
</div>

<div mt-8 grid grid-cols-2 gap-8>

<v-click>
<div class="bg-white/5 backdrop-blur-sm border border-white/10 rounded-lg p-6">
  <div class="text-2xl mb-4">🎯 핵심 특징</div>
  <div class="space-y-3">
    <div class="flex items-center">
      <div class="w-2 h-2 bg-blue-400 rounded-full mr-3"></div>
      <span>프롬프트 엔지니어링 기반</span>
    </div>
    <div class="flex items-center">
      <div class="w-2 h-2 bg-green-400 rounded-full mr-3"></div>
      <span>소스 그라운딩 (Source Grounding)</span>
    </div>
    <div class="flex items-center">
      <div class="w-2 h-2 bg-purple-400 rounded-full mr-3"></div>
      <span>긴 문서 최적화</span>
    </div>
    <div class="flex items-center">
      <div class="w-2 h-2 bg-orange-400 rounded-full mr-3"></div>
      <span>LLM 세계 지식 활용</span>
    </div>
  </div>
</div>
</v-click>

<v-click>
<div class="bg-white/5 backdrop-blur-sm border border-white/10 rounded-lg p-6">
  <div class="text-2xl mb-4">⚡ 기술적 장점</div>
  <div class="space-y-3">
    <div class="flex items-center">
      <div class="w-2 h-2 bg-cyan-400 rounded-full mr-3"></div>
      <span>Few-shot 학습 지원</span>
    </div>
    <div class="flex items-center">
      <div class="w-2 h-2 bg-pink-400 rounded-full mr-3"></div>
      <span>병렬 처리 및 청킹</span>
    </div>
    <div class="flex items-center">
      <div class="w-2 h-2 bg-lime-400 rounded-full mr-3"></div>
      <span>높은 재현율 보장</span>
    </div>
    <div class="flex items-center">
      <div class="w-2 h-2 bg-amber-400 rounded-full mr-3"></div>
      <span>구조화된 출력 제공</span>
    </div>
  </div>
</div>
</v-click>

</div>

---
class: py-10
glowSeed: 180
---

<div flex justify-between items-start>
  <div>
    <h1>Ollama: 로컬 LLM의 혁신</h1>
    <span>개인 컴퓨터에서 실행하는 최신 언어모델</span>
  </div>
  <img src="/ollama-hero.png" alt="Ollama" class="h-24 rounded-lg shadow-2xl">
</div>

<div mt-8 grid grid-cols-2 gap-6>

<v-click>
<div class="bg-white/5 backdrop-blur-sm border border-white/10 rounded-lg p-6">
  <div class="text-xl mb-4 flex items-center">
    <div class="i-carbon:security text-2xl mr-2 text-green-400"></div>
    <span class="text-green-400">프라이버시 & 보안</span>
  </div>
  <div class="space-y-2 text-sm">
    <div>• 민감한 데이터가 외부로 전송되지 않음</div>
    <div>• 완전한 데이터 통제권 확보</div>
    <div>• GDPR, CCPA 등 규정 준수</div>
  </div>
</div>
</v-click>

<v-click>
<div class="bg-white/5 backdrop-blur-sm border border-white/10 rounded-lg p-6">
  <div class="text-xl mb-4 flex items-center">
    <div class="i-carbon:cost text-2xl mr-2 text-blue-400"></div>
    <span class="text-blue-400">비용 절감 & 효율성</span>
  </div>
  <div class="space-y-2 text-sm">
    <div>• API 호출 비용 제로</div>
    <div>• 오프라인 환경에서 작업 가능</div>
    <div>• 무제한 추출 작업 실행</div>
  </div>
</div>
</v-click>

<v-click>
<div class="bg-white/5 backdrop-blur-sm border border-white/10 rounded-lg p-6">
  <div class="text-xl mb-4 flex items-center">
    <div class="i-carbon:settings text-2xl mr-2 text-purple-400"></div>
    <span class="text-purple-400">맞춤화 & 제어</span>
  </div>
  <div class="space-y-2 text-sm">
    <div>• Llama 3, Gemma 등 다양한 모델 지원</div>
    <div>• Modelfile을 통한 모델 커스터마이징</div>
    <div>• 간편한 설치 및 API 제공</div>
  </div>
</div>
</v-click>

<v-click>
<div class="bg-white/5 backdrop-blur-sm border border-white/10 rounded-lg p-6">
  <div class="text-xl mb-4 flex items-center">
    <div class="i-carbon:development text-2xl mr-2 text-orange-400"></div>
    <span class="text-orange-400">개발자 친화적</span>
  </div>
  <div class="space-y-2 text-sm">
    <div>• 간단한 명령어로 모델 실행</div>
    <div>• RESTful API 엔드포인트 제공</div>
    <div>• 다양한 프로그래밍 언어 지원</div>
  </div>
</div>
</v-click>

</div>

---
class: py-10
glowSeed: 125
---

# 목표: Secure Extract PII

<span>민감한 데이터를 외부에 보내지 않는 안전한 PII 추출</span>

<div mt-8 />

<div flex justify-center mb-6>
  <img src="/pii.png" alt="PII Protection" class="w-70 rounded-lg shadow-xl">
</div>

<div grid grid-cols-3 gap-6>

<v-click>
<div class="bg-gradient-to-br from-blue-900/30 to-cyan-900/30 border border-blue-800/50 rounded-xl p-6">
  <div class="text-3xl mb-3 text-center">🎯</div>
  <div class="text-xl font-bold text-blue-300 mb-3 text-center">유연성</div>
  <div class="text-sm text-center space-y-2">
    <div>새로운 PII 유형 발견 시</div>
    <div class="text-blue-400">모델 재학습 없이</div>
    <div>프롬프트 수정으로 대응</div>
  </div>
</div>
</v-click>

<v-click>
<div class="bg-gradient-to-br from-green-900/30 to-emerald-900/30 border border-green-800/50 rounded-xl p-6">
  <div class="text-3xl mb-3 text-center">✅</div>
  <div class="text-xl font-bold text-green-300 mb-3 text-center">검증 가능성</div>
  <div class="text-sm text-center space-y-2">
    <div>추출된 정보의 출처를</div>
    <div class="text-green-400">원본 텍스트에서 추적</div>
    <div>시각적 검증 지원</div>
  </div>
</div>
</v-click>

<v-click>
<div class="bg-gradient-to-br from-purple-900/30 to-pink-900/30 border border-purple-800/50 rounded-xl p-6">
  <div class="text-3xl mb-3 text-center">🔒</div>
  <div class="text-xl font-bold text-purple-300 mb-3 text-center">데이터 프라이버시</div>
  <div class="text-sm text-center space-y-2">
    <div>민감한 PII가</div>
    <div class="text-purple-400">외부 클라우드로 전송되지 않음</div>
    <div>로컬 환경에서만 처리</div>
  </div>
</div>
</v-click>

</div>

---
class: py-10
glowSeed: 200
---

# 기술 스택: 완벽한 조합

<span>LangExtract + Ollama = 보안과 성능의 만남</span>

<div mt-8 />

<div flex justify-center gap-8 items-center>

<v-click>
<div class="bg-white/5 backdrop-blur-sm border border-white/10 rounded-xl p-8 text-center">
  <div class="text-6xl mb-4">🔎</div>
  <div class="text-xl font-bold text-blue-300 mb-2">LangExtract</div>
  <div class="text-sm opacity-80">Google의 LLM 기반<br>정보 추출 라이브러리</div>
</div>
</v-click>

<v-click>
<div class="text-6xl text-green-400">+</div>
</v-click>

<v-click>
<div class="bg-white/5 backdrop-blur-sm border border-white/10 rounded-xl p-8 text-center">
  <div class="text-6xl mb-4">🦙</div>
  <div class="text-xl font-bold text-orange-300 mb-2">Ollama</div>
  <div class="text-sm opacity-80">로컬 환경에서<br>LLM을 실행하는 도구</div>
</div>
</v-click>

<v-click>
<div class="text-6xl text-purple-400">=</div>
</v-click>

<v-click>
<div class="bg-gradient-to-br from-green-900/30 to-blue-900/30 border border-green-800/50 rounded-xl p-8 text-center">
  <div class="text-4xl mb-4">🛡️</div>
  <div class="text-xl font-bold text-green-300 mb-2">Secure PII Extraction</div>
  <div class="text-sm text-green-400 space-y-1">
    <div>✓ 외부 의존성 제거</div>
    <div>✓ 완전한 데이터 통제</div>
    <div>✓ 유연한 확장성</div>
  </div>
</div>
</v-click>

</div>

---
class: py-10
glowSeed: 150
---

# 실험: 46개 PII 항목 추출

<span>포괄적인 개인식별정보 추출 범위</span>

<div mt-6 />

<div grid grid-cols-4 gap-3 text-sm>

<v-click>
<div class="bg-blue-900/20 border border-blue-800/50 rounded p-3">
  <div class="font-bold text-blue-300 mb-2">👤 개인 정보</div>
  <div class="space-y-1 text-xs">
    <div>• 이름 (Name)</div>
    <div>• 나이 (Age)</div>
    <div>• 생년월일</div>
    <div>• 성별 (Gender)</div>
    <div>• 결혼 여부</div>
    <div>• 신체적 특징</div>
  </div>
</div>
</v-click>

<v-click>
<div class="bg-green-900/20 border border-green-800/50 rounded p-3">
  <div class="font-bold text-green-300 mb-2">📱 연락처</div>
  <div class="space-y-1 text-xs">
    <div>• 이메일 주소</div>
    <div>• 전화번호</div>
    <div>• 주소 (Address)</div>
    <div>• 우편번호</div>
    <div>• IP 주소</div>
    <div>• 웹사이트 주소</div>
  </div>
</div>
</v-click>

<v-click>
<div class="bg-purple-900/20 border border-purple-800/50 rounded p-3">
  <div class="font-bold text-purple-300 mb-2">🆔 식별 번호</div>
  <div class="space-y-1 text-xs">
    <div>• 주민등록번호</div>
    <div>• 운전면허증 번호</div>
    <div>• 여권 번호</div>
    <div>• 건강보험 번호</div>
    <div>• 계좌 번호</div>
    <div>• 차량 식별 번호</div>
  </div>
</div>
</v-click>

<v-click>
<div class="bg-orange-900/20 border border-orange-800/50 rounded p-3">
  <div class="font-bold text-orange-300 mb-2">🏢 사회적 정보</div>
  <div class="space-y-1 text-xs">
    <div>• 직업 (Occupation)</div>
    <div>• 조직 (Organization)</div>
    <div>• 의료 기관</div>
    <div>• 정치 성향</div>
    <div>• 종교 (Religion)</div>
    <div>• 출신 (Origin)</div>
  </div>
</div>
</v-click>

</div>

<div v-click mt-6>
<div class="bg-gradient-to-r from-red-900/20 to-pink-900/20 border border-red-800/50 rounded-lg p-4">
  <div class="text-lg font-bold text-red-300 mb-2 flex items-center">
    <div class="i-carbon:warning text-xl mr-2"></div>
    특히 민감한 PII 항목들
  </div>
  <div class="grid grid-cols-3 gap-4 text-sm">
    <div>• 성적 지향 (Sexuality)</div>
    <div>• 별자리 (Zodiac Sign)</div>
    <div>• 의료 전문가 이름</div>
  </div>
</div>
</div>

---
class: py-10
glowSeed: 175
---

# 워크플로 1: 프롬프트 설계

<span>명확하고 구체적인 추출 규칙 정의</span>

<div mt-8 />

<div class="bg-white/5 backdrop-blur-sm border border-white/10 rounded-lg overflow-hidden">

<v-click>
<div class="bg-blue-900/30 px-4 py-2 flex items-center">
  <div class="i-carbon:edit text-xl mr-2"></div>
  <span class="font-bold">프롬프트 설계 전략</span>
</div>
</v-click>

<v-click>
<div class="px-4 py-2">
  <div class="bg-gray-800 rounded-lg p-3 font-mono text-xs">
    <div class="text-green-400"># 핵심 지시사항</div>
    <div class="mt-1 space-y-0.5">
      <div><span class="text-blue-400">prompt_description</span> = <span class="text-yellow-400">"""</span></div>
      <div class="ml-3">Extract all 46 types of Personally Identifiable Information (PII)</div>
      <div class="ml-3">in their order of appearance.</div>
      <div class="ml-3 mt-1 text-orange-400"># 정확성 보장을 위한 규칙</div>
      <div class="ml-3">- Use the exact text for extractions</div>
      <div class="ml-3">- Do not paraphrase or overlap entities</div>
      <div class="ml-3">- Provide meaningful attributes for context</div>
      <div><span class="text-yellow-400">"""</span></div>
    </div>
  </div>
</div>
</v-click>

</div>

<div v-click mt-6>
<div class="grid grid-cols-3 gap-4">
  <div class="bg-green-900/20 border border-green-800/50 rounded-lg p-4">
    <div class="text-lg font-bold text-green-300 mb-2">✓ 순서 보장</div>
    <div class="text-sm">등장 순서대로 PII 추출</div>
  </div>
  <div class="bg-blue-900/20 border border-blue-800/50 rounded-lg p-4">
    <div class="text-lg font-bold text-blue-300 mb-2">✓ 정확한 텍스트</div>
    <div class="text-sm">의역하지 않고 원문 그대로</div>
  </div>
  <div class="bg-purple-900/20 border border-purple-800/50 rounded-lg p-4">
    <div class="text-lg font-bold text-purple-300 mb-2">✓ 컨텍스트 제공</div>
    <div class="text-sm">의미 있는 속성 추가</div>
  </div>
</div>
</div>

---
class: py-10
glowSeed: 185
---

# 워크플로 2: Few-shot 예시 작성

<span>고품질 학습 데이터로 모델 성능 향상</span>

<div mt-6 />

<div grid grid-cols-2 gap-6>

<v-click>
<div class="bg-white/5 backdrop-blur-sm border border-white/10 rounded-lg overflow-hidden">
  <div class="bg-blue-900/30 px-4 py-2 flex items-center">
    <div class="i-carbon:document text-lg mr-2"></div>
    <span class="font-bold text-sm">예시 1: 한국어 일반 프로필</span>
  </div>
  <div class="px-4 py-3 text-xs font-mono">
    <div class="text-gray-300 mb-2">입력 텍스트:</div>
    <div class="bg-gray-800 rounded p-2 text-xs mb-3">
      이름은 <span class="bg-red-900/50">홍길동</span>(남성, <span class="bg-blue-900/50">35세</span>)이며,
      <span class="bg-green-900/50">서울</span> 출신입니다.<br>
      주민등록번호는 <span class="bg-purple-900/50">900101-1234567</span>이고,<br>
      연락처는 <span class="bg-orange-900/50">010-1234-5678</span>
    </div>
    <div class="text-gray-300 mb-2">추출 결과:</div>
    <div class="bg-gray-800 rounded p-2 text-xs space-y-1">
      <div>• Name: "홍길동"</div>
      <div>• Age: "35세"</div>
      <div>• Location: "서울"</div>
      <div>• SSN: "900101-1234567"</div>
    </div>
  </div>
</div>
</v-click>

<v-click>
<div class="bg-white/5 backdrop-blur-sm border border-white/10 rounded-lg overflow-hidden">
  <div class="bg-green-900/30 px-4 py-2 flex items-center">
    <div class="i-carbon:hospital text-lg mr-2"></div>
    <span class="font-bold text-sm">예시 2: 영어 의료 기록</span>
  </div>
  <div class="px-4 py-3 text-xs font-mono">
    <div class="text-gray-300 mb-2">입력 텍스트:</div>
    <div class="bg-gray-800 rounded p-2 text-xs mb-3">
      Patient <span class="bg-red-900/50">John Smith</span>, a US citizen,<br>
      visited Dr. <span class="bg-blue-900/50">Emily White</span><br>
      at <span class="bg-green-900/50">Seoul Mercy Hospital</span>
      on <span class="bg-purple-900/50">2025-09-18</span>
    </div>
    <div class="text-gray-300 mb-2">추출 결과:</div>
    <div class="bg-gray-800 rounded p-2 text-xs space-y-1">
      <div>• Name: "John Smith"</div>
      <div>• Medical Professional: "Emily White"</div>
      <div>• Medical Facility: "Seoul Mercy Hospital"</div>
      <div>• Date: "2025-09-18"</div>
    </div>
  </div>
</div>
</v-click>

</div>

<div v-click mt-6>
<div class="bg-gradient-to-r from-yellow-900/20 to-orange-900/20 border border-yellow-800/50 rounded-lg px-4 py-2">
  <div class="text-lg font-bold text-yellow-300 mb-2 flex items-center">
    <div class="i-carbon:lightbulb text-xl mr-2"></div>
    Few-shot 학습의 핵심
  </div>
  <div class="text-sm grid grid-cols-2 gap-2">
    <div>• 다양한 언어와 도메인 커버</div>
    <div>• 일관성 있는 구조화된 출력</div>
    <div>• 복잡한 모델 훈련 없이 성능 향상</div>
    <div>• 실제 사용 케이스 반영</div>
  </div>
</div>
</div>

---
class: py-10
clicks: 4
glowSeed: 195
---

# 워크플로 3: 추출 실행 및 최적화

<span>성능과 정확도를 위한 파라미터 튜닝</span>

<div mt-4 />

<div class="bg-white/5 backdrop-blur-sm border border-white/10 rounded-lg overflow-hidden">

<v-click>
<div class="bg-purple-900/30 px-4 py-2 flex items-center">
  <div class="i-carbon:settings text-lg mr-2"></div>
  <span class="font-bold">LangExtract 설정</span>
</div>
</v-click>

<div class="px-4 py-2">
<v-click>
<div class="bg-gray-800 rounded-lg p-3 font-mono text-xs">
<div class="text-blue-400">result</div> = <div class="text-green-400">lx.extract</div>(<br>
<div class="ml-4">
  <div><span class="text-yellow-400">model_id</span>=<span class="text-orange-400">"gemma3:4b"</span>,</div>
  <div><span class="text-yellow-400">model_url</span>=<span class="text-orange-400">"http://localhost:11434"</span>,</div>
  <div class="mt-2 text-cyan-400"># 성능 최적화 파라미터</div>
  <div><span class="text-yellow-400">extraction_passes</span>=<span class="text-red-400">3</span>,  <span class="text-gray-400"># 재현율 향상</span></div>
  <div><span class="text-yellow-400">max_workers</span>=<span class="text-red-400">3</span>,      <span class="text-gray-400"># 병렬 처리</span></div>
  <div><span class="text-yellow-400">max_char_buffer</span>=<span class="text-red-400">1000</span>, <span class="text-gray-400"># 정확도 향상</span></div>
</div>
)
</div>
</v-click>

</div>
</div>

<div v-click mt-3>
<div class="grid grid-cols-2 gap-4">
  <div class="bg-white/5 backdrop-blur-sm border border-white/10 rounded-lg px-4 py-2">
    <div class="text-base font-bold text-red-300 mb-1">기본 설정 성능</div>
    <div class="space-y-1 text-sm">
      <div class="text-xs flex justify-between">
        <span>추출된 PII 수:</span>
        <span class="text-red-400">18개</span>
      </div>
      <div class="text-xs flex justify-between">
        <span>소요 시간:</span>
        <span class="text-yellow-400">32초</span>
      </div>
      <div class="text-xs flex justify-between">
        <span>오탐률:</span>
        <span class="text-red-400">2개</span>
      </div>
    </div>
  </div>

  <div class="bg-white/5 backdrop-blur-sm border border-white/10 rounded-lg px-4 py-2">
    <div class="text-base font-bold text-green-300 mb-1">최적화된 설정</div>
    <div class="space-y-2 text-sm">
      <div class="text-xs flex justify-between">
        <span>추출된 PII 수:</span>
        <span class="text-green-400">21개</span>
      </div>
      <div class="text-xs flex justify-between">
        <span>소요 시간:</span>
        <span class="text-yellow-400">56초</span>
      </div>
      <div class="text-xs flex justify-between">
        <span>오탐률:</span>
        <span class="text-green-400">0개</span>
      </div>
    </div>
  </div>
</div>
</div>

<div v-click class="absolute inset-0 flex items-center justify-center">
<div class="bg-blue-900 border border-blue-800/50 rounded-lg px-6 py-8">
  <div class="text-center text-blue-300 font-bold">
    ⚡ 설정 조정만으로도 정확도 16% 향상, 오탐 완전 제거!
  </div>
</div>
</div>

---
class: py-10
glowSeed: 210
---

# 실행 환경 및 결과

<span>실제 테스트 환경과 성능 지표</span>

<div mt-4 />

<div grid grid-cols-2 gap-8>

<v-click>
<div class="bg-white/5 backdrop-blur-sm border border-white/10 rounded-lg p-6">
  <div class="text-xl font-bold text-blue-300 mb-3 flex items-center">
    <div class="i-carbon:chip text-2xl mr-2"></div>
    실행 환경
  </div>
  <div class="space-y-2 text-sm">
    <div class="flex justify-between">
      <span class="text-gray-400">OS:</span>
      <span>Windows 11</span>
    </div>
    <div class="flex justify-between">
      <span class="text-gray-400">CPU:</span>
      <span>AMD Ryzen 2700X</span>
    </div>
    <div class="flex justify-between">
      <span class="text-gray-400">GPU:</span>
      <span>NVIDIA RTX 2070</span>
    </div>
    <div class="flex justify-between">
      <span class="text-gray-400">RAM:</span>
      <span>32GB</span>
    </div>
    <div class="flex justify-between">
      <span class="text-gray-400">Python:</span>
      <span>3.12</span>
    </div>
    <div class="flex justify-between">
      <span class="text-gray-400">Model:</span>
      <span class="text-green-400">Gemma 3 4B</span>
    </div>
  </div>
</div>
</v-click>

<v-click>
<div class="bg-white/5 backdrop-blur-sm border border-white/10 rounded-lg p-6">
  <div class="text-xl font-bold text-green-300 mb-3 flex items-center">
    <div class="i-carbon:chart-line text-2xl mr-2"></div>
    최종 성능 결과
  </div>
  <div class="space-y-2">
    <div class="bg-green-900/20 border border-green-800/50 rounded p-3">
      <div class="text-sm font-bold text-green-400">21개 PII 추출 성공</div>
      <div class="text-xs text-gray-400">32개 중 65.7% 검출</div>
    </div>
    <div class="bg-blue-900/20 border border-blue-800/50 rounded p-3">
      <div class="text-sm font-bold text-blue-400">오탐율 0%</div>
      <div class="text-xs text-gray-400">완벽한 정확도 달성</div>
    </div>
    <div class="bg-purple-900/20 border border-purple-800/50 rounded p-3">
      <div class="text-sm font-bold text-purple-400">56초 처리 시간</div>
      <div class="text-xs text-gray-400">로컬 환경 최적화 완료</div>
    </div>
  </div>
</div>
</v-click>

</div>

<div v-click mt-4>
<div class="bg-gradient-to-r from-green-900/30 to-blue-900/30 border border-green-800/50 rounded-lg p-4">
  <div class="text-center">
    <div class="text-xl font-bold text-green-300 mb-2">🎉 성공적인 PoC 완료!</div>
    <div>
      <a href="https://huketo.github.io/extract-pii-poc" target="_blank" class="text-blue-400 hover:text-blue-300 underline">
        📊 실시간 추출 결과 시각화 확인하기
      </a>
    </div>
  </div>
</div>
</div>

---
class: py-10
glowSeed: 225
---

# 시각화 결과: Source Grounding

<span>추출된 PII의 투명하고 검증 가능한 추적</span>

<div mt-4 />

<div class="flex justify-center mb-6">
  <img src="/extract-pii-poc-result-screen.png" alt="PII Extraction Results" class="rounded-lg shadow-2xl h-64">
</div>

<div v-click>
<div class="grid grid-cols-3 gap-4">
  <div class="bg-green-900/20 border border-green-800/50 rounded-lg p-4">
    <div class="text-lg font-bold text-green-300 mb-2 flex items-center">
      <div class="i-carbon:view text-xl mr-2"></div>
      시각적 하이라이팅
    </div>
    <div class="text-sm">원본 텍스트에서 추출된 PII가 색상별로 구분되어 표시</div>
  </div>

  <div class="bg-blue-900/20 border border-blue-800/50 rounded-lg p-4">
    <div class="text-lg font-bold text-blue-300 mb-2 flex items-center">
      <div class="i-carbon:cursor-1 text-xl mr-2"></div>
      대화형 검증
    </div>
    <div class="text-sm">하이라이트된 텍스트에 호버하면 속성과 분류 정보 확인</div>
  </div>

  <div class="bg-purple-900/20 border border-purple-800/50 rounded-lg p-4">
    <div class="text-lg font-bold text-purple-300 mb-2 flex items-center">
      <div class="i-carbon:document-attachment text-xl mr-2"></div>
      소스 추적
    </div>
    <div class="text-sm">모든 추출 결과가 정확한 원본 위치와 연결되어 검증 가능</div>
  </div>
</div>
</div>

---
class: py-10
glowSeed: 240
---

# 성과 및 혁신점

<span>기존 방식 대비 획기적인 개선사항</span>

<div mt-8 />

<div grid grid-cols-2 gap-8>

<v-click>
<div class="bg-white/5 backdrop-blur-sm border border-white/10 rounded-lg p-6">
  <div class="text-2xl font-bold text-green-300 mb-4">✨ 주요 성과</div>
  <div class="space-y-4">
    <div class="flex items-start">
      <div class="i-carbon:time text-lg text-blue-400 mr-3 mt-1"></div>
      <div>
        <div class="font-bold text-blue-300">신속한 개발 사이클</div>
        <div class="text-sm text-gray-400">수개월 모델 재학습 → 프롬프트 수정으로 즉시 대응</div>
      </div>
    </div>
    <div class="flex items-start">
      <div class="i-carbon-checkmark-outline text-lg text-green-400 mr-3 mt-1"></div>
      <div>
        <div class="font-bold text-green-300">높은 검증 가능성</div>
        <div class="text-sm text-gray-400">소스 그라운딩과 시각화로 신뢰성 확보</div>
      </div>
    </div>
    <div class="flex items-start">
      <div class="i-carbon:security text-lg text-purple-400 mr-3 mt-1"></div>
      <div>
        <div class="font-bold text-purple-300">최고 수준 데이터 보안</div>
        <div class="text-sm text-gray-400">로컬 처리로 외부 유출 위험 원천 차단</div>
      </div>
    </div>
  </div>
</div>
</v-click>

<v-click>
<div class="bg-white/5 backdrop-blur-sm border border-white/10 rounded-lg p-6">
  <div class="text-2xl font-bold text-orange-300 mb-4">🚀 혁신점</div>
  <div class="space-y-4">
    <div class="flex items-start">
      <div class="i-carbon:hybrid-networking text-lg text-cyan-400 mr-3 mt-1"></div>
      <div>
        <div class="font-bold text-cyan-300">하이브리드 접근법</div>
        <div class="text-sm text-gray-400">LLM의 강력함 + 로컬 실행의 안전함</div>
      </div>
    </div>
    <div class="flex items-start">
      <div class="i-carbon:repeat text-lg text-yellow-400 mr-3 mt-1"></div>
      <div>
        <div class="font-bold text-yellow-300">무제한 재사용</div>
        <div class="text-sm text-gray-400">API 비용 걱정 없이 반복 실행 가능</div>
      </div>
    </div>
    <div class="flex items-start">
      <div class="i-carbon:tools text-lg text-pink-400 mr-3 mt-1"></div>
      <div>
        <div class="font-bold text-pink-300">개발자 친화적</div>
        <div class="text-sm text-gray-400">Python 생태계와 완벽 통합</div>
      </div>
    </div>
  </div>
</div>
</v-click>

</div>

<div v-click mt-6>
<div class="bg-gradient-to-r from-blue-900/30 to-purple-900/30 border border-blue-800/50 rounded-lg p-4">
  <div class="text-center">
    <div class="text-xl font-bold text-blue-300 mb-2">
      💡 핵심 가치 제안
    </div>
    <div class="text-lg">
      <span class="text-green-400">보안성</span> + <span class="text-blue-400">유연성</span> + <span class="text-purple-400">검증가능성</span> =
      <span class="text-yellow-400 font-bold">차세대 PII 추출 솔루션</span>
    </div>
  </div>
</div>
</div>

---
class: py-10
glowSeed: 255
---

# 한계점 및 개선 방향

<span>솔직한 평가와 향후 발전 계획</span>

<div mt-8 />

<div grid grid-cols-2 gap-8>

<v-click>
<div class="bg-red-900/20 border border-red-800/50 rounded-lg p-6">
  <div class="text-xl font-bold text-red-300 mb-4">⚠️ 현재 한계점</div>
  <div class="space-y-3">
    <div class="flex items-start">
      <div class="i-carbon:timer text-lg text-orange-400 mr-3 mt-1"></div>
      <div>
        <div class="font-bold text-orange-300">성능 최적화 필요</div>
        <div class="text-sm text-gray-400">정확도와 처리 시간 간 균형 조정 요구</div>
      </div>
    </div>
    <div class="flex items-start">
      <div class="i-carbon:model text-lg text-yellow-400 mr-3 mt-1"></div>
      <div>
        <div class="font-bold text-yellow-300">모델 의존성</div>
        <div class="text-sm text-gray-400">LLM과 프롬프트 품질에 성능이 크게 의존</div>
      </div>
    </div>
    <div class="flex items-start">
      <div class="i-carbon:data-1 text-lg text-red-400 mr-3 mt-1"></div>
      <div>
        <div class="font-bold text-red-300">실시간 처리 제약</div>
        <div class="text-sm text-gray-400">현재는 배치 처리에 최적화됨</div>
      </div>
    </div>
  </div>
</div>
</v-click>

<v-click>
<div class="bg-green-900/20 border border-green-800/50 rounded-lg p-6">
  <div class="text-xl font-bold text-green-300 mb-4">🎯 개선 방향</div>
  <div class="space-y-3">
    <div class="flex items-start">
      <div class="i-carbon:speed text-lg text-blue-400 mr-3 mt-1"></div>
      <div>
        <div class="font-bold text-blue-300">성능 최적화</div>
        <div class="text-sm text-gray-400">GPU 가속, 모델 경량화 등 최적화 기법 적용</div>
      </div>
    </div>
    <div class="flex items-start">
      <div class="i-carbon:earth text-lg text-cyan-400 mr-3 mt-1"></div>
      <div>
        <div class="font-bold text-cyan-300">다국어 지원 강화</div>
        <div class="text-sm text-gray-400">다양한 언어와 문화적 맥락 지원</div>
      </div>
    </div>
    <div class="flex items-start">
      <div class="i-carbon:flow text-lg text-purple-400 mr-3 mt-1"></div>
      <div>
        <div class="font-bold text-purple-300">파이프라인 통합</div>
        <div class="text-sm text-gray-400">기존 데이터 워크플로와의 완벽한 통합</div>
      </div>
    </div>
  </div>
</div>
</v-click>

</div>

<div v-click mt-8>
<div class="bg-blue-900/20 border border-blue-800/50 rounded-lg p-4">
  <div class="text-lg font-bold text-blue-300 mb-2 text-center">
    📈 확장 가능성
  </div>
  <div class="text-center text-sm">
    <span class="text-green-400">의료</span> • <span class="text-blue-400">법률</span> • <span class="text-purple-400">금융</span>
    등 다양한 산업 분야로 확장 가능한 범용 프레임워크
  </div>
</div>
</div>

---
class: py-10
glowSeed: 270
---

# 로드맵: 단계적 발전 계획

<span>PoC에서 프로덕션까지의 여정</span>

<div mt-4 />

<div class="relative">

<v-click>
<div class="flex items-center mb-4">
  <div class="w-8 h-8 bg-green-500 rounded-full flex items-center justify-center text-white font-bold">✓</div>
  <div class="ml-4 flex-1">
    <div class="text-lg font-bold text-green-300">Phase 1: Extract PII PoC</div>
    <div class="text-sm text-gray-400">기술 검증 완료 (Jupyter Notebook)</div>
  </div>
  <div class="text-sm text-green-400 font-bold">COMPLETED</div>
</div>
</v-click>

<v-click>
<div class="flex items-center mb-4">
  <div class="w-8 h-8 bg-blue-500 rounded-full flex items-center justify-center text-white font-bold">2</div>
  <div class="ml-4 flex-1">
    <div class="text-lg font-bold text-blue-300">Phase 2: Extract PII MVP</div>
    <div class="text-sm text-gray-400 space-y-1">
      <div>• Desktop App (Flet) 또는 API 서비스 (FastAPI) 개발</div>
      <div>• 사용자 친화적 GUI 인터페이스 제공</div>
      <div>• 배치 처리 및 결과 관리 기능</div>
    </div>
  </div>
  <div class="text-sm text-yellow-400 font-bold">IN PLANNING</div>
</div>
</v-click>

<v-click>
<div class="flex items-center mb-4">
  <div class="w-8 h-8 bg-purple-500 rounded-full flex items-center justify-center text-white font-bold">3</div>
  <div class="ml-4 flex-1">
    <div class="text-lg font-bold text-purple-300">Phase 3: Extract PII Extension</div>
    <div class="text-sm text-gray-400 space-y-1">
      <div>• Browser Extension (TypeScript + React)</div>
      <div>• 웹 페이지에서 실시간 PII 감지</div>
      <div>• Desktop App/API 서비스와 연동</div>
    </div>
  </div>
  <div class="text-sm text-gray-400 font-bold">FUTURE</div>
</div>
</v-click>

</div>

<div v-click mt-4>
<div class="bg-gradient-to-r from-purple-900/30 to-pink-900/30 border border-purple-800/50 rounded-lg p-4">
  <div class="text-center">
    <div class="text-xl font-bold text-purple-300 mb-2">🚀 비전</div>
    <div class="text-lg">
      누구나 쉽게 사용할 수 있는 <span class="text-green-400">안전한 PII 추출 솔루션</span>으로 발전
    </div>
    <div class="text-sm text-gray-400 mt-2">
      개발자부터 비개발자까지 모든 사용자를 위한 포괄적 생태계 구축
    </div>
  </div>
</div>
</div>

---
layout: center
class: text-center
---

# 결론: 새로운 패러다임의 시작

<div class="mt-8 text-xl opacity-80">
  LangExtract + Ollama = 안전하고 유연한 PII 추출의 미래
</div>

<div class="mt-8 grid grid-cols-3 gap-6">

<v-click>
<div class="bg-gradient-to-br from-blue-900/30 to-cyan-900/30 border border-blue-800/50 rounded-xl p-6">
  <div class="text-4xl mb-3">🛡️</div>
  <div class="text-lg font-bold text-blue-300">보안성</div>
  <div class="text-sm text-gray-400">민감한 데이터의<br>완전한 로컬 처리</div>
</div>
</v-click>

<v-click>
<div class="bg-gradient-to-br from-green-900/30 to-emerald-900/30 border border-green-800/50 rounded-xl p-6">
  <div class="text-4xl mb-3">⚡</div>
  <div class="text-lg font-bold text-green-300">효율성</div>
  <div class="text-sm text-gray-400">프롬프트 수정으로<br>즉시 대응 가능</div>
</div>
</v-click>

<v-click>
<div class="bg-gradient-to-br from-purple-900/30 to-pink-900/30 border border-purple-800/50 rounded-xl p-6">
  <div class="text-4xl mb-3">🎯</div>
  <div class="text-lg font-bold text-purple-300">정확성</div>
  <div class="text-sm text-gray-400">소스 그라운딩으로<br>검증 가능한 결과</div>
</div>
</v-click>

</div>

<div v-click class="mt-8 text-center">
  <div class="bg-gradient-to-r from-yellow-900/20 to-orange-900/20 border border-yellow-800/50 rounded-lg px-8 py-4 inline-block">
    <div class="text-2xl font-bold text-yellow-300">
      데이터 프라이버시 시대의 필수 솔루션
    </div>
  </div>
</div>

---
layout: center
class: text-center
---

# 감사합니다

<div class="mt-8 text-xl opacity-80">
  질문이나 피드백을 환영합니다!
</div>

<div class="mt-12 grid grid-cols-2 gap-8 max-w-120 mx-auto">
  <div class="bg-white/5 backdrop-blur-sm border border-white/10 rounded-lg p-6">
    <div class="text-lg font-bold text-blue-300 mb-3">🔗 참고 자료</div>
    <div class="text-sm space-y-2">
      <div>• <a href="https://github.com/google/langextract" class="text-blue-400 hover:text-blue-300">LangExtract GitHub</a></div>
      <div>• <a href="https://ollama.com" class="text-blue-400 hover:text-blue-300">Ollama 공식 사이트</a></div>
      <div>• <a href="https://huketo.github.io/extract-pii-poc" class="text-blue-400 hover:text-blue-300">데모 결과 확인</a></div>
    </div>
  </div>

  <div class="bg-white/5 backdrop-blur-sm border border-white/10 rounded-lg p-6">
    <div class="text-lg font-bold text-green-300 mb-3">⚙️ 기술 스택</div>
    <div class="text-sm space-y-2">
      <div>• Python 3.12</div>
      <div>• LangExtract (Google)</div>
      <div>• Ollama + Gemma 3 4B</div>
      <div>• Jupyter Notebook</div>
    </div>
  </div>
</div>
