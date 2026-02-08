# LLM

## 1. [Ollama](https://ollama.com)
- LLM을 쉽게 설치하고 관리하기 위해 Ollama라는 프로그램을 사용
- 로컬 환경에서 AI 모델을 간편하게 사용할 수 있게 도와주는 도구
- 명령어 한줄만 입력하면 원하는 AI 모델을 바로 설치하고 사용 가능

### Quick Start  
> % curl -fsSL https://ollama.com/install.sh | sh    # 설치
> % sudo systemctl start ollama   # 정지  
> % systemctl status ollama      # 상태 확인  
> % sudo systemctl stop ollama   # 정지
> % ollama list                  # 설치된 모델 조회
> % ollama pull {modle name}     # ex. qwen3:0.6b, gpt-oss:20b

### 1-1. CLI
> % ollama run {modle name}      # 설치/실행
> % /bye                         # 대화 중단
> % ollama run gpt-oss:20b "양자 컴퓨팅을 간단한 용어로 설명해 줘"  # 대화형 없이 빠른 응답을 원하는 경우

### 1-2. API


### 1-3. Web prompt

<br>

## 2. [gpt-oss](https://openai.com/ko-KR/open-models/)
- OpenAI의 오픈웨이트(open weight) 모델
- license: Apach 2.0 
- [gpt-oss no install](https://gpt-oss.com/)
- [output price](https://openrouter.ai/)

### 2-1. 권장사양  
> - gpt-oss-120b: ram(60gb), vram(16gb/24gb)  
> - gpt-oss-20b: ram(16gb), vram(80gb/96gb)  

### 2-2. 커스터마이징
- Ollama의 Modelfile을 사용하면 재훈련 없이 GPT-OSS 동작을 맞춤 설정할 수 있다.
- 시스템 프롬프트를 설정하거나, 컨텍스트 크기를 조정하거나, 매개변수를 미세 조정할 수 있다.

#### Modelfile 생성
> FROM gpt-oss:20b  
SYSTEM "You are a technical assistant specializing in Python programming. Provide concise, accurate code with comments."  
PARAMETER temperature 0.5  
PARAMETER num_ctx 4096

#### 사용자 정의 모델 빌드
- Modelfile 이 있는 경로에서 실행
> $ ollama create python-gpt-oss -f Modelfile  
> $ ollama run python-gpt-oss





















