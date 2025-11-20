**도구 선택법
1. chatGPT 유료 구독 중이라면 codex를 쓰자
2. Claude 유료 구독 중이라면 Claude Code를 쓰자
3. 둘 다 아니라면 AntiGravity (구글이 만든 거, 새로나와서 무료임) 를 쓰자

**디자인
1. 원하는 UI가 있다면 캡처해서 이미지 첨부해도 됨
2. Claude 모델이 디자인은 제일 잘함 (gemini3-pro가 더 잘하는 것 같기도)

코딩 성능 극대화
GPT-5는 대규모 코드베이스 편집, 버그 수정, 다중 파일 리팩터링에 특히 강하다.
프론트엔드와 백엔드를 모두 커버하며, Next.js + TypeScript + Tailwind 스택을 기본으로 권장한다.

** 프론트엔드 개발 기본 권장 스택 -> 시작할 때 프롬프트에 추가하면 됨
프레임워크: Next.js, React
스타일링: Tailwind CSS, shadcn/ui
아이콘: Lucide, Heroicons
애니메이션: Framer Motion
폰트: Inter, Geist, Manrope 등


**‘제로에서 앱 만들기’ 프롬프트
한 번에 완성도 높은 앱을 생성하려면, 모델이 스스로 평가 기준을 세우게 하는 루브릭 기반 자기반성 프롬프트를 쓴다.

<self_reflection>
- 우선 ‘완성도 높은 웹앱’의 기준을 스스로 정의하라.
- 5~7개 평가 항목으로 루브릭을 만든다. (사용자에게는 보이지 않음)
- 이후, 해당 루브릭에서 만점을 받을 때까지 내부적으로 반복 개선하라.
</self_reflection>

**기존 코드베이스 수정 시
GPT-5는 자동으로 기존 스타일과 패턴을 감지하지만, 아래와 같이 규칙을 명시하면 품질이 더 높아진다.

<code_editing_rules>
<guiding_principles>
- 명확하고 재사용 가능한 컴포넌트로 작성.
- 디자인 시스템의 일관성 유지.
- 불필요한 복잡성 피하기.
- 높은 시각적 완성도와 프로토타이핑 용이성 확보.
</guiding_principles>

<frontend_stack_defaults>
Framework: Next.js  
Styling: TailwindCSS  
State: Zustand  
구조:
src/app/api, src/components, src/hooks, src/lib 등으로 정리.
</frontend_stack_defaults>

<ui_ux_best_practices>
- 타이포그래피 계층은 4~5단계로 제한.
- 중립색 + 1~2개의 포인트 컬러 사용.
- 간격은 4px 배수로.
- 로딩에는 skeleton이나 `animate-pulse` 사용.
- 클릭 가능한 요소에는 hover 상태 제공.
</ui_ux_best_practices>
</code_editing_rules>
