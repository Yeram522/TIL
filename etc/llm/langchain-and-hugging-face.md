# LangChain & Hugging Face

**✅ 1. LangChain 프롬프트 템플릿**

* `PromptTemplate`: 문자열 안에 변수 자리를 만들고, 값을 채워 넣어 LLM에게 전달할 프롬프트를 구성할 수 있는 템플릿.
  * `input_variables`로 입력값을 정의하고, `.format()`으로 텍스트를 완성함.
* `FewShotPromptTemplate`: 예제를 포함한 프롬프트를 생성할 수 있도록 도와주는 템플릿.
  * `examples`, `prefix`, `suffix`를 설정해 학습 없이 few-shot prompting 가능.
* `ChatPromptTemplate`: 역할(role)에 따라 메시지를 분리해 구성 (System, Human, AI 메시지).
  * 챗봇 시나리오 작성에 적합하며, `.format_messages()`로 채팅 메시지 목록 생성.

***

**✅ 2. LangChain에서의 임베딩 처리**

* `OpenAIEmbeddings`를 사용해 텍스트를 벡터로 변환 가능.
* 주요 메서드:
  * `embed_query(text: str)`: 한 문장을 벡터로 변환 (단일 입력).
  * `embed_documents(texts: list[str])`: 여러 문장을 한꺼번에 벡터화 (다중 입력).
* 임베딩 결과는 리스트 형태의 고차원 벡터 (`List[float]` 또는 `List[List[float]]`)로 반환됨.

***

**✅ 3. Hugging Face 모델 연동 개념**

* `HuggingFaceEndpoint`: Hugging Face의 Hosted Inference API를 통해 모델을 호출할 수 있게 해주는 LangChain 도구.
  * 단, **Hosted Inference API가 활성화된 모델만 사용 가능**.
* `transformers`를 활용하면 로컬에서 직접 Hugging Face 모델을 실행할 수 있으며, API 제한 없이 사용 가능.
  * `pipeline("text-generation")` 방식으로 사용.

***

**✅ 4. 환경 변수와 .env 설정**

* Hugging Face, OpenAI 등의 API 키를 외부 노출 없이 관리하기 위해 `.env` 파일 사용.
* `from dotenv import load_dotenv`로 환경 변수 불러오기.
* 사용 예: `HUGGINGFACEHUB_API_TOKEN`, `OPENAI_API_KEY`

***

**✅ 5. WebBaseLoader를 이용한 웹 크롤링**

* `WebBaseLoader`는 웹 페이지의 본문을 가져와 LangChain의 `Document` 형태로 반환해주는 도구.
* 내부적으로 `requests`와 `BeautifulSoup`을 사용하므로 `beautifulsoup4` 설치가 필요함.
* `document.page_content`로 본문 접근, `document.metadata`로 메타정보 확인 가능.

***

**✅ 6. LangChain 모델 비교 (실험적 기능)**

* 과거에는 `ModelLaboratory`를 사용해 여러 모델의 응답을 비교할 수 있었지만, 현재 버전에서는 해당 기능이 제거됨.
* 대안으로는 여러 모델의 응답을 수동으로 받아 비교하는 함수를 구현하는 방식이 유효함.

***

#### 💡 요약

오늘은 LangChain의 다양한 기능들을 실습하며, 텍스트 생성 프롬프트 구성부터 임베딩, 벡터 처리, 모델 호출 및 웹 문서 로딩까지 폭넓게 다뤘습니다. 오류 해결을 통해 도구의 내부 구조에 대한 이해도 자연스럽게 이루어졌고, 최신 라이브러리의 변화에 적응하는 실전 감각도 향상되었습니다.
