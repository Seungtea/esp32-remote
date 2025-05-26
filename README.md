# ESP32 MQTT 제어 시스템

ESP32와 MQTT를 사용하여 센서 데이터를 모니터링하고 액추에이터(서보 모터, LED, LCD)를 제어하는 시스템입니다.

## 1. 시스템 구성

- **ESP32**: 센서 데이터 수집 및 액추에이터 제어
- **MQTT 브로커**: 메시지 중개 (Mosquitto 또는 HiveMQ)
- **웹 인터페이스**: 사용자 제어 및 모니터링

## 2. 파일 구성

- `boot.py`: ESP32 부팅 시 실행되는 WiFi 연결 코드
- `main.py`: ESP32 메인 애플리케이션 코드
- `esp32_control.html`: 웹 인터페이스
- `mosquitto.conf`: 로컬 Mosquitto MQTT 브로커 설정 파일 (선택사항)

## 3. MQTT 브로커 옵션

이 시스템은 두 가지 MQTT 브로커 옵션을 지원합니다:

### 옵션 1: 공개 HiveMQ 브로커 (초보자 권장)

- **장점**: 설치 없이 바로 사용 가능, 인터넷만 있으면 어디서나 액세스 가능
- **설정 방법**: 기본적으로 main.py와 esp32_control.html에 HiveMQ 설정이 되어 있어 별도 설정 필요 없음
- **주의사항**: 공개 브로커이미로 다른 사용자도 메시지를 볼 수 있음, 중요 데이터는 전송하지 마세요

### 옵션 2: 로컬 Mosquitto 브로커

- **장점**: 개인 네트워크에서만 액세스 가능하여 보안성 높음, 전송 지연 적음
- **설치 방법**: README의 Mosquitto 설치 안내를 참고하여 설치
- **코드 수정**: main.py와 esp32_control.html에서 공개 브로커 설정을 주석 처리하고 로컬 브로커 설정을 활성화

## 4. 설치 및 설정 가이드

### 4.1 ESP32 설정

1. Thonny IDE 설치: [Thonny 공식 웹사이트](https://thonny.org/) 에서 다운로드

2. ESP32에 MicroPython 펌웨어 설치:
   - Thonny IDE에서 `도구 > 인터프리터...` 선택
   - ESP32 선택 후 `MicroPython 설치...` 버튼 클릭

3. 필요한 라이브러리 설치: Thonny의 쉘 창에서 실행
   ```python
   import upip
   upip.install('umqtt.simple')
   ```

4. 코드 수정 및 업로드:
   - `boot.py`: WiFi SSID와 비밀번호 변경
   - `main.py`: 지정된 MQTT 브로커 확인 (HiveMQ 또는 로컬)
   - 파일들을 ESP32에 업로드

### 4.2 웹 인터페이스 설정

1. `esp32_control.html` 파일을 웹 브라우저에서 열기

2. 브로커 설정 확인:
   - 공개 HiveMQ 사용 시: 기본 설정 유지
   - 로컬 Mosquitto 사용 시: JavaScript 코드에서 브로커 설정 수정

## 5. 사용 방법

### 5.1 HiveMQ 브로커 사용 시

1. ESP32 전원 연결 및 WiFi 연결 확인
2. 웹 브라우저에서 `esp32_control.html` 파일 열기
3. 웹 인터페이스에서 연결 버튼 클릭 후 제어 시작

### 5.2 로컬 Mosquitto 사용 시

1. Mosquitto 브로커 실행 (관리자 권한으로):
   ```
   net start mosquitto
   ```
2. ESP32 전원 연결
3. 웹 브라우저에서 `esp32_control.html` 파일 열기
4. 웹 인터페이스에서 연결 버튼 클릭 후 제어 시작

## 6. 문제 해결

- **WiFi 연결 문제**: boot.py의 WiFi 설정 확인
- **MQTT 연결 문제**: 브로커 주소와 포트 정확히 설정 확인
- **센서 오류**: 핀 연결 확인 및 main.py의 예외 처리 로그 확인

## 7. 추가 정보

- 이 시스템은 ESP32 위에서 실행되는 MicroPython을 사용합니다.
- 인터넷을 통한 원격 제어를 위해 공개 HiveMQ 브로커를 사용할 수 있습니다.
- 공개 브로커 사용 시 중요 데이터나 개인 정보는 전송하지 마세요.

이 설명서는 다른 에이전트의 제안을 반영하여 초보자도 쉽게 사용할 수 있도록 하였습니다.
