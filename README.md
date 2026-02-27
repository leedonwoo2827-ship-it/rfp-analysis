# RFP Analyzer - AI 제안서 RFP 분석 스킬

발주처 RFP 문서(PDF)에서 제안서 구조를 자동으로 분석하고 요구사항을 추출하는 Claude Desktop 스킬입니다.

## 주요 기능

- **Backbone 자동 생성**: PDF 내의 제목 패턴(1., Ⅰ., ①, ■ 등)을 분석하여 제안서의 전체 뼈대(Lv1, Lv2) 구성
- **계층 구조 정밀도 향상**: 단어 단위로 쪼개진 항목을 병합하거나 재분리하여 논리적인 문단 구조로 정제
- **요구사항 파악**: 기술 스펙, 관리 요구사항 등 제안서에서 반드시 답변해야 할 핵심 키워드 추출

## 설치 방법

### 방법 1: 드래그 앤 드롭 (권장)

1. 이 레포지토리를 클론하거나 ZIP으로 다운로드합니다:
   ```bash
   git clone https://github.com/leedonwoo2827-ship-it/rfp-analyzer.git
   ```

2. Claude Desktop을 실행합니다.

3. `rfp-analyzer` 폴더를 Claude Desktop 창에 드래그 앤 드롭합니다.

4. 스킬이 자동으로 설치되며, Claude가 사용 가능하다고 알려줍니다.

### 방법 2: 수동 설치

Claude Desktop의 Skills 디렉토리에 직접 복사:

**Windows:**
```bash
xcopy /E /I rfp-analyzer "%APPDATA%\Claude\skills\rfp-analyzer"
```

**macOS/Linux:**
```bash
cp -r rfp-analyzer ~/.config/Claude/skills/
```

## 사용 방법

### 기본 사용

Claude Desktop에서 자연스럽게 요청하세요:

```
"이 RFP 파일을 분석해서 제안서 구조를 만들어줘"
```

```
"제안요청서에서 필수 작성 항목을 뽑아줘"
```

### Claude Desktop 프로젝트에서 사용

`claude_desktop_config.json` 또는 프로젝트 지침에 다음을 추가:

```json
{
  "instructions": "RFP 분석이 필요할 때는 rfp_analysis 스킬을 사용하세요."
}
```

### 통합 제안서 자동화 프로젝트에서 사용

이 스킬은 다음 스킬들과 함께 사용하면 완전한 제안서 자동화가 가능합니다:

1. **rfp-analyzer** (이 스킬) - RFP 분석 및 구조 추출
2. **company-data-manager** - 회사 자료 관리
3. **proposal-writer** - 제안서 초안 작성
4. **hwpx-writer** - HWPX 파일 생성
5. **text2img-mcp** - 이미지 생성 (MCP)

## 예제

### RFP 분석 요청

```
사용자: 이 RFP 파일을 분석해서 제안서 뼈대를 만들어줘
        [RFP.pdf 업로드]

Claude: RFP 분석을 시작하겠습니다.

1단계: PDF 텍스트 추출 중...
2단계: 제목 패턴 분석 중...
3단계: 계층 구조 생성 중...

분석 완료! 다음과 같은 구조를 추출했습니다:

Lv1. 사업 개요
  Lv2. 사업 목적
  Lv2. 추진 배경

Lv1. 과정 설계
  Lv2. 훈련 과정명
  Lv2. 교육 내용
  ...
```

## 활용 팁

### 1. PDF 품질
- 텍스트 기반 PDF에서 가장 잘 작동합니다
- 이미지로 스캔된 PDF는 OCR 전처리가 필요할 수 있습니다

### 2. 구조 검토
- 자동 추출된 구조는 반드시 검토 후 사용하세요
- 필요시 수동으로 조정할 수 있습니다

### 3. 다음 단계
- 추출된 구조를 `company-data-manager`와 `proposal-writer`로 전달하여 자동 작성

## 기술 스택

- PDF 파싱: `pdf-parse` 라이브러리 활용
- 계층 구조 분석: 휴리스틱 알고리즘
- 출력 형식: 구조화된 JSON

## 주의 사항

- 텍스트가 아닌 이미지 형식으로 구성된 PDF의 경우 뼈대 추출이 제한될 수 있습니다
- 추출된 뼈대는 반드시 사용자의 검토를 거쳐 최종 작성본으로 확정해야 합니다

## 라이선스

MIT License

## 기여

이슈나 개선 제안은 GitHub Issues를 통해 제출해주세요.

## 관련 프로젝트

- [company-data-manager](https://github.com/leedonwoo2827-ship-it/company-data-manager) - 회사 자료 관리 스킬
- [proposal-writer](https://github.com/leedonwoo2827-ship-it/proposal-writer) - 제안서 작성 스킬
- [hwpx-writer](https://github.com/leedonwoo2827-ship-it/hwpx-writer) - HWPX 생성 스킬
- [text2img-mcp](https://github.com/leedonwoo2827-ship-it/text2img-mcp) - 이미지 생성 MCP
