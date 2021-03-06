# Role 디렉토리 구조
- defaults: 룰에서 사용하는 변수의 기본값 정의
- files: 작업 대상 호스트에 복사할 파일을 배치할 디렉토리
- handlers: 핸들러로 사용할 태스크 정의
- meta: 룰의 의존 관계 정의
- tasks: 룰에서 실행할 태스크 정의
- templates: 작업 대상 호스트에 활용할 진자2 템플릿 배치
- tests: 룰을 테스트하기 위한 플레이북(test.yml)과 인벤토리 정의(inventory) 배치
- vars: 룰에서 사용할 변수 정의

태스크와 변수 등을 정의하기 위해 YAML 파일이 필요한 디렉터리에는 main.yml 파일이 만들어져 있다.
defaults와 vars는 모두 변수를 정의하기 위한 디렉토리지만, defaults에는 우선순위가 가장 낮은(=변경 할 수 있는) 변수를 정의하고, vars에는 변경할 수 없는(=개별적으로 변경할 수 없는) 인벤토리 변수를 정의한다.
이처럼 롤은 사전에 "역할이 정해진" 디렉토리 구조로 구성되고, 각 디렉토리에는 그 역할에 맞게 파일을 작성해야 하며,
`ansible-galaxy init` 명령으로 간단하게 초기화 할 수 있다.

***

# Role 변수 설정

## 롤 안의 변수는 롤 이름으로 시작하기
롤 안에서 정의되는 변수 이름은 롤 이름을 변수 이름 맨 앞에 붙인다.


## 변수의 기본 값을 지정 - defaults 폴더
변수의 값을 플레이북에서 설정하고 싶으면 기본밗을 설정하지 않은 채로 둘 수 있겠지만, 앞서 변수로 구성한 항목이라면 롤에서 기본값을 설정하는 것이 좋다.

***

# nginx reload용 핸들러 추가
설졍 변경 사항을 반영하려면 nginx 서비스를 리로드해야 한다. 리로드 하려면 service 모듈의 state 옵션에 reloaded를 지정하면 된다. 다만 리로드나 재시작 계열의 작업은 다른 설정이 처리된 후에 "맨 마지막에 한번만" 실행해야 한다.
그래서 앤서블에는 핸들러(Handler)라는 지연 실행 전용으로 태스크를 정의하는 방법이 있다.

## 핸들러 특징
- 롤의 handlers/main.yml 또는 플레이의 handlers 지시자에 정의한다.
- 핸들러는 일반적인 태스크의 notify 지시자에서 등록할 수 있다.
- 핸들러는 notify한 태스크가 변경과 관련된 처리를 수행한 경우에만 등록될 수 있다.
- 등록된 핸들러는 플레이 실행에서 맨 마지막에 한 번만 실행된다.
