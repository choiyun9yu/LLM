# LLM

## 1. [Ollama](https://ollama.com)
- LLM을 쉽게 설치하고 관리하기 위해 Ollama라는 프로그램을 사용
- 로컬 환경에서 AI 모델을 간편하게 사용할 수 있게 도와주는 도구
- 명령어 한줄만 입력하면 원하는 AI 모델을 바로 설치하고 사용 가능

### Quick Start
~~~
% curl -fsSL https://ollama.com/install.sh | sh    # 설치
% sudo systemctl start ollama   # 정지  
% systemctl status ollama      # 상태 확인  
% sudo systemctl stop ollama   # 정지
% ollama list                  # 설치된 모델 조회
% ollama pull {modle name}     # ex. qwen3:0.6b, gpt-oss:20b
~~~

### 1-1. CLI
~~~
% ollama run {modle name}      # 설치/실행
% /bye                         # 대화 중단
% ollama run gpt-oss:20b "양자 컴퓨팅을 간단한 용어로 설명해 줘"  # 대화형 없이 빠른 응답을 원하는 경우
~~~

### 1-2. API

#### POST /api/generate: 단일 프롬프트에 대한 텍스트를 생성
~~~
% curl http://localhost:11434/api/generate -H "Content-Type: application/json" -d '{"model": "gpt-oss:20b", "prompt": "REST API를 위한 Python 스크립트를 작성해 줘"}'
~~~

#### POST /api/chat: 메시지 기록을 통한 대화형 상호 작용을 지원
~~~
% curl http://localhost:11434/v1/chat/completions -H "Content-Type: application/json" -d '{"model": "gpt-oss:20b", "messages": [{"role": "user", "content": "신경망에 대해 설명해 줘"}]}'
~~~

####  OpenAPI 호환성
~~~python
from openai import OpenAI
client = OpenAI(base_url="http://localhost:11434/v1", api_key="ollama")
response = client.chat.completions.create(
    model="gpt-oss:20b",
    messages=[{"role": "user", "content": "머신러닝이 뭐야?"}]
)
print(response.choices[0].message.content)
~~~

<br>

#### 외부 포트 포워딩
~~~ 
% netstat -tuln     # 포트 수신 상태 조회
~~~
- 127.0.0.1:portnumber 면 로컬에서 오는 요청만 듣고
- 0.0.0.0:portNumber 면 외부에서 오는 요청도 들을 수 있음

~~~
% sudo systemctl edit ollama

[Service]
Environment="OLLAMA_HOST=0.0.0.0:11434"
ctrl + o -> Enter -> ctrl + x

% sudo systemctl restart ollama
~~~


### 1-3. Web prompt (GUI)

#### Open Web UI
~~~
% docker run -d -p 3000:8080 --name open-webui ghcr.io/open-webui/open-webui:main    # install
% docker logs -f open-webui    # info check
~~~
- localhost:3000



<br>

## 2. [gpt-oss](https://openai.com/ko-KR/open-models/)
- OpenAI의 오픈웨이트(open weight) 모델
- license: Apach 2.0 
- [gpt-oss no install](https://gpt-oss.com/)
- [output price](https://openrouter.ai/)

### 2-1. 권장사양  
- gpt-oss-120b: ram(60gb), vram(16gb/24gb)    
- gpt-oss-20b: ram(16gb), vram(80gb/96gb)     

### 2-2. 커스터마이징
- Ollama의 Modelfile을 사용하면 재훈련 없이 GPT-OSS 동작을 맞춤 설정할 수 있다.
- 시스템 프롬프트를 설정하거나, 컨텍스트 크기를 조정하거나, 매개변수를 미세 조정할 수 있다.

#### Modelfile 생성
~~~
touch Modelfile    
nano Modilfile
~~~
  
> FROM gpt-oss:20b    # 어떤 모델을 사용할지 지정    
> SYSTEM "You are a technical assistant specializing in Python programming.   
> Provide concise, accurate code with comments."    # 설정 프롬프트     
> PARAMETER temperature 0.5    # 창의성(0-1, 높을 수록 창의성 높고, 낮을 수록 진실된 답변)     
> PARAMETER num_ctx 4096       # (ctx, Token Context)  

#### 사용자 정의 모델 빌드
- Modelfile 이 있는 경로에서 실행
~~~
% ollama create python-gpt-oss -f Modelfile    # 사용자가 정의한 모델 파일 생성  
% ollama run python-gpt-oss                    # 빌드한 파일 실행  
~~~

<br>

## 3. Embedding Model
→ multilingual-e5-base


<br>

## 4. Rerank Model
→ mmarco-mMiniLMv2-L12




















