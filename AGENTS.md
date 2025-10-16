# 레포지토리 가이드라인

## 프로젝트 구조 및 모듈 구성
런타임 코드는 `src/puzzle_game/`에 위치하며 `core`, `ui`, `puzzles` 서브패키지로 구성됩니다. 레벨 정의는 `content/levels/*.json`에 보관하고 정적 아트/오디오는 `assets/`에 저장합니다. 공유 유틸리티는 `src/puzzle_game/common/`에 위치해야 합니다. 테스트는 `tests/` 하위에서 패키지 레이아웃을 미러링합니다 (`src/puzzle_game/puzzles/slider.py` <-> `tests/puzzles/test_slider.py`).

## 빌드, 테스트 및 개발 명령어
`python -m venv .venv`로 가상 환경을 생성하고 `.venv\Scripts\Activate.ps1`로 활성화합니다. `pip install -r requirements.txt`로 의존성을 설치합니다. `python -m puzzle_game`으로 게임을 로컬에서 실행합니다. `pytest`로 전체 테스트 스위트를 실행하고 푸시 전에 `pytest --maxfail=1 --disable-warnings`를 추가하세요. `ruff check .`와 `black .`을 사용하여 포매팅 일관성을 유지합니다.

## 코딩 스타일 및 명명 규칙
Python 3.11+ 대상으로 작성합니다. 4칸 들여쓰기를 사용하고, 함수와 변수는 `snake_case`, 클래스는 `PascalCase`를 사용합니다. 모듈 이름은 디렉토리와 일치시킵니다 (`src/puzzle_game/ui/menu.py`). 레벨 JSON 파일은 소문자와 하이픈으로 된 이름을 유지합니다 (`content/levels/ice-caves.json`). 커밋 전에 `black`과 `ruff`를 실행하세요. 설정은 `pyproject.toml`에 있습니다.

## 테스트 가이드라인
`pytest-cov`와 함께 `pytest`를 사용합니다. 기여분은 커버리지를 85% 이상 유지해야 합니다. 테스트 모듈은 `test_<주제>.py`로 명명하고 픽스처는 `tests/conftest.py`에 배치합니다. 새로운 퍼즐 메커니즘의 경우 단위 커버리지와 `puzzle_loader`를 통해 퍼즐을 로드하는 통합 테스트를 모두 포함해야 합니다. 개발 중에는 `pytest -k`를 사용하여 범위를 지정합니다.

## 커밋 및 풀 리퀘스트 가이드라인
Conventional Commits을 따릅니다 (`feat: add gravity toggle`). 제목 줄은 72자 이하로 유지하고 본문에 이유를 설명합니다. 각 PR에는 간결한 요약, 테스트 증거 (`pytest`, `ruff`, `black`), 관련 이슈 또는 디자인 문서 링크를 포함해야 합니다. UI 변경이 게임플레이에 영향을 미치는 경우 스크린샷 또는 GIF를 첨부하세요. 병합 전에 최소 한 명의 관리자로부터 리뷰를 받으세요.

## 설정 및 에셋
절대 비밀 정보를 커밋하지 마세요. 환경 키는 `.env`에 배치하고 `.env.example`에 문서화합니다. 체크인 전에 텍스처와 오디오를 최적화하고, 소스 에셋은 무손실 형식을 선호합니다. 대용량 바이너리는 `assets/raw/`에 넣고 내보내기 준비된 버전은 `assets/processed/`에 저장합니다.
