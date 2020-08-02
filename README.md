# relay_02

# 기획서

### 후보 서비스
[후보 서비스 목록](https://github.com/boostcamp-2020/relay_02/blob/master/LatteChallenge.md)

- 선택된 서비스 : 스카이 러브

## 스카이 러브

## 시나리오

0. 회원가입을 합니다. (선택)

1. ID, PW를 입력하여 로그인을 합니다. (필수 - 기능 A)
2. 왼쪽에 프로필 사진을 추가합니다. (필수 - 기능 B) 
프로필 설정을 수정할 수도 있어요. (선택)
3. 가운데 공간에서 스카이러브가 상대를 추천해줍니다. (필수 - 기능 A, C)
4. 왼쪽의 사람(리스트)를 클릭하면, 오른쪽에 상대방의 프로필이 나옵니다. (필수 - 기능 A, C / 선택 - 블러 기능)
(필수 - 기능 A, C)
5. 상대방의 프로필 설명에는 스카이러브의 추천 이유가 포함됩니다. (선택 - 기능 C)
6. 추천 리스트에 있는 상대를 클릭하고, 들어가기 버튼을 누르면 채팅방으로 입장합니다. 
(필수 - 기능 A)
7. 채팅이 이루어지고 나면, 언행점수가 변화합니다. (필수 - 기능 A)
채팅을 통해 얻은 자연어를 기반으로 단어 파싱을 진행하여 & 긍정/부정을 인식을 통해 사용자의 성향을 파악합니다.
8. 채팅에서 나가려면 나가기 버튼을 클릭합니다. (필수 - 기능 A)


## 가이드 UI
- 메인 화면
![function](https://user-images.githubusercontent.com/49153756/89023391-77e36800-d35e-11ea-9fe1-ca3629989ea8.png)

- 로그인
![login](https://user-images.githubusercontent.com/49153756/89024554-41a6e800-d360-11ea-9ee4-a6eb8656682f.png)

- 회원가입
![signup](https://user-images.githubusercontent.com/49153756/89024548-3fdd2480-d360-11ea-9a05-9f9a8d075c8b.png)

## 기능 A

**[ 기반 기능 ]**

[0. 회원 정보 DB 생성](https://github.com/boostcamp-2020/relay_02/blob/master/%ED%9A%8C%EC%9B%90%EC%A0%95%EB%B3%B4.md)

1. 로그인 기능을 구현한다.
2. 실시간 채팅을 구현한다.
3. 채팅이 종료되면 대화 패턴 긍정도 분석을 통해 언행 점수를 평가한다.

**[대화 패턴 긍정도 분석 기능]**

매칭 후 채팅에서 누적된 긍정, 부정 대화 패턴 데이터를 이용해 긍정도 점수를 db에 저장한다.

(display용은 아니고 분석 시 데이터로만 활용)

- 사용자들이 채팅에서 대화를 끝내면 각 대화 thread 수집
- 사용자에게 자연어가 들어오면 단어 단위로 파싱
- 수집된 정보를 바탕으로 단어 파싱 & 긍정/부정 인식 (자연어 처리)
- 사용자의 긍정 단어 사용 점수를 DB에 저장
→ 추후 점수가 비슷한 사용자들끼리 매칭 서비스에 이용

**[기반 기능 (선택)]**

1. 회원가입 기능 구현


**[추천 툴]**
- 채팅 기능을 위한 서버 - [socket.io](http://socket.io/)
- 채팅 내용을 분석하기 위한 한글 형태소 분석기 - 은전 한닢

## 기능 B

**[기반 기능]**

1. 프로필 사진 업로드 기능을 구현한다.
2. 업로드된 프로필 사진을 동물상 기반 추천 기능에 적용하고, DB에 저장한다.

**[동물상 기반 추천 기능(필수)]**

- 사용자의 프로필 사진을 기반으로 어떤 동물 상일지 분석한다.

    → 공룡상, 고양이상, 강아지상, 여우상, 곰상, 토끼상 etc.

- 사용자의 동물상이 회원 정보에 등록된다. *(*기능 A의 회원정보 DB 생성 참고)*
- 사용자가 선호하는 이상형의 동물상을 입력한다.
- 선호하는 동물상의 사람과 매칭될 수 있도록 한다.

    : 해당 매칭 과정은 C에서 이루어지도록 한다.

**[프로필 이미지 가리기 기능(선택)]**
- **아래 두 개 중 택1 하여 구현**
```
[얼굴 블러 기능 (선택)]

- 사용자가 자신의 프로필 사진을 업로드한다.
- 사진을 분석하여 얼굴 부분에 블러 처리를 한다.
- 블러 처리된 이미지를 DB에 저장한다.
- 서로의 동의 하에 얼굴을 공개할 수 있다.

[기본 이미지 동물상으로 표시 기능(선택)]

- '동물상 기반 추천 기능(필수)' 에서 얻은 동물상을 기본 프로필 이미지로 설정되도록 한다.
- 서로의 동의 하에 얼굴을 공개할 수 있다.
```

**[기획 배경]**

- 상대방의 호기심 유발
- 성격을 중요하게 생각하는 사람들을 대상으로 함

**[추천 툴]**

- OpenCV
- Clova API (부스트캠퍼니까 ㅎ..)
- Face API
    - [https://romeoh.tistory.com/entry/face-api-face-apijs-for-Browser](https://romeoh.tistory.com/entry/face-api-face-apijs-for-Browser)
- Face detection 관련 자료는 많으니 다양하게 이용하시면 됩니다.
- 동물상 분석 관련: [https://www.youtube.com/watch?v=OI3fZJHQF8Y](https://www.youtube.com/watch?v=OI3fZJHQF8Y&t=307s)

## 기능 C

**[기반 기능]**
1. 각종 개인정보 입력이 가능한 프로필 설정 구현
2. 정보 기반 이성 추천 기능(호감도 평가) 구현

[**회원 정보 기반 이성 추천 기능(필수)]**
- 분석에 필요한 정보
    - 회원 정보를 활용해서 적합한 이성을 추천함 *(*기능 A의 회원 정보 DB 생성하기 참고)*
    - [나이, 성격 , 취미, 주소(거리 측정을 위함), mbti, 차량유무, 이상형 얼굴형, 프로필 사진, 언행 점수] 중에 추가 및 수정 가능
- 분석의 흐름
    1. 위 항목을 토대로 DB에서 분석에 필요한 정보를 추출
    2. 그 정보들을 분석하고 호감도 점수 계산
    3. 계산된 점수를 기반으로 적합한 이성을 추천

**[기반 기능(선택)]**
1. 스카이러브의 추천 이유 안내 구현


