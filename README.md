# 새티스팩토리 모딩 문서

새티스팩토리 모드 로더(SML) 및 새티스팩토리 모딩에 대한 문서입니다.
마스터 분기는 <https://docs.ficsit.app/>에서 운영 중입니다.
질문이나 제안이 있으면 [새티스팩토리 모딩 디스코드 서버](https://discord.gg/xkVJ73E)에 문의하거나 풀 리퀘스트(아래 참조)를 통해 기여해 주세요.

우리는 소스 파일에서 [의미적 줄 바꿈 형식](https://sembr.org/)을 사용하려고 시도하고 있지만 사용하나 마나의 수준입니다.

풀 요청은 `Dev` 분기를 대상으로 해야 합니다.

변경 사항을 제출하기 전에 아래 개발 설정 지침에 따라 페이지가 예상대로 표시되는지 확인해야 합니다.

다른 모드에 대한 문서도 동일한 사이트를 통해 제공됩니다.
모드에 대한 문서를 작성했고 이를 추가하고 싶다면 당사에 문의해주세요.

## 기여

문서에 대한 귀하의 기여에 크게 감사드립니다.
페이지의 대략적인 개요만 완성한 경우에도 디스코드에서 저희에게 연락하시면
전체 페이지로 전환할 수 있도록 도와드리겠습니다.

기여하는 가장 쉬운 방법은 저장소를 포크한 다음 `Dev` 분기를 대상으로 하는 풀 리퀘스트를 사용하여 변경 사항을 검토하는 것입니다.

1~2일 이내에 검토하지 않으면 디스코드로 메시지를 보내주세요.

## 개발자 설정

### 개발 컨테이너

비주얼 스튜디오 코드 및 Docker가 이미 설치되어 있는 경우 VSCode에서 폴더를 열 때 자동 감지되는 저장소에 대한 [개발 컨테이너](https://code.visualstudio.com/docs/devcontainers/containers)를 제공합니다.

이것은 깃허브 코드스페이스에서도 지원되겠지만 테스트해 본 적은 없습니다.

컨테이너는 브라우저 또는 VSCode 내에서 미리보기를 위해 열 때 빌드된 콘텐츠를 자동으로 제공합니다.

### 수동

미리 구성된 개발 컨테이너 또는 코드스페이스를 사용하지 않으려면 아래 지침을 따르세요.

거의 모든 편집기를 사용하여 `.adoc` 파일을 편집할 수 있지만 Visual Studio Code([Asciidoc](https://marketplace.visualstudio.com/items?itemName=asciidoctor.asciidoctor-vscode) 및 [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker) 확장 사용 추천) 또는 IntelliJ를 사용하는 것이 좋습니다.

배포하기 전에 라이브 사이트에서 페이지가 어떻게 보이는지 확인하려면 아래 지침을 따르세요.

#### 설치

1. 원하는 방법으로 [Node.js](https://nodejs.org/en/download/) 및 [Yarn Package Manager](https://classic.yarnpkg.com/en/docs/install)를 설치합니다.

2. Yarn을 사용하여 종속성을 설치합니다.

```bash
yarn install
```

#### 빌드

SML 및 기타 모든 호스트된 모드에 대한 문서를 빌드하려면:

```bash
yarn run build
```

참고로 좀 걸릴 겁니다.

혹은 SML용 문서를 빌드하려면 대체 [Antora 플레이북 파일](https://cdn.discordapp.com/attachments/629385164115673108/689142080043352073/antora-playbook-dev.yml)을 다운로드하여 저장소 폴더에 넣습니다.

그런 다음 다음을 실행합니다.

```bash
yarn run build:dev
```

두 명령어의 출력 HTML 파일은 `\build\site` 에서 찾을 수 있습니다.

#### 미리보기

콘텐츠를 미리 보려면 브라우저에서 출력 HTML 파일을 열 수 있습니다. 예. `build/site/satisfactory-modding/latest/index.html`

`yarn serve` 를 실행하여 로컬 웹 서버를 시작할 수도 있습니다.

## 다른 모드의 문서 추가

원하는 경우 다른 모드에 대한 문서를 작성하여 라이브 사이트에 포함시킬 수 있습니다.

이를 수행한 모드에는 FicsIt-Networks, Refined Power, Ficsit Remote Monitoring, TweakIt 등이 있습니다.

이를 설정하려면 자세한 내용을 문의해주세요. 일반적인 단계는 다음과 같습니다.

- 문서 파일로 저장소 만들기
- 저장소에서 [github 작업 활성화](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository)
- `antora-playbook-ci.yml` 및 `antora-playbook.yml` 파일을 편집하여 저장소를 소스로 추가하세요. 이미 나열된 다른 모드의 형식을 따라야 합니다.
- 사이트를 소스로 추가하여 이 문서 저장소를 로컬에서 빌드할 수 있는지 확인하세요. 이를 위해 `package.json` 에 정의된 `build` 작업을 실행합니다. 속도를 높이려면 일시적으로 다른 모드의 저장소를 주석 처리하는 것이 좋습니다.
- 배포된 사본이 저장소에 변경 사항을 푸시할 때 자동으로 업데이트되도록 하려면 [이 파일](.github/workflows/SubModPush.yml.example)과 유사한 작업 파일을 설정하고 디스코드에서 문의하여 [비밀에 추가](https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository)할 토큰을 받아야 합니다. 작업 파일이 작동할 수 있습니다.
- 플레이북 파일에 대한 변경 사항으로 `Dev` 분기를 풀리퀘합니다.

## 새 버전 분기 추가

일반적으로 SML의 새 주 버전 또는 부 버전이 출시되면 새 버전 분기를 만듭니다.
목표는 문서에서 이전 버전으로 작업하기 위한 참조 지점을 제공하는 것입니다.

문서의 새 고정 버전 분기를 추가하려면...

1. `vX.X.X` 이름 형식(예: `v3.1.1`)에 따라 `master` 분기의 커밋에 태그를 만듭니다.
2. HEAD 항목 뒤 `antora-playbook.yml` 및 `antora-playbook-ci.yml` 의 분기 목록 앞에 태그 이름을 추가합니다.
3. 준비가 되었습니다. CI가 자동으로 배포를 처리합니다.
