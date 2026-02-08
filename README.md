# LLM

## 1. [Ollama](https://ollama.com)
- LLM을 쉽게 설치하고 관리하기 위해 Ollama라는 프로그램을 사용
- 로컬 환경에서 AI 모델을 간편하게 사용할 수 있게 도와주는 도구
- 명령어 한줄만 입력하면 원하는 AI 모델을 바로 설치하고 사용 가능

### Quick Start  
> % curl -fsSL https://ollama.com/install.sh | sh    # 설치  
> % systemctl status ollama      # 상태 확인  
> % ollama list                  # 설치된 모델 조회
> % ollama pull {modle name}     # ex. qwen3:0.6b  
> % ollama run {modle name}      # 설치/실행
> % /bye                         # 대화 중단
> % sudo systemctl stop ollama   # 정지  
