<div align='center'>
  
최근에 혼자서 클론코딩하며 연습하고 있는 프로젝트가 있는데,

굉장히 쉽고 간단한데 한번도 보지못했던 에러 핸들링 방법이 있어서

미리 정리해두려고 한다.

<img src='https://blog.kakaocdn.net/dn/btYsF5/btrH0OJChj0/Snso63f3TgUY6mfmQqrBKk/img.png' />
  
index.js


미들웨어를 사용하는 index.js 파일에서 위와 같은 식을 미리 만들어두고

<img src='https://blog.kakaocdn.net/dn/c6Jk8b/btrHZCDtTRh/4w1T2SsEUGpEqupmL1KnMk/img.png' />

utils/error.js

어느 파일에서도 간단하게 불러올 수 있게 utils폴더에 error.js 파일을 만들어 관리해준다.

<img src='https://blog.kakaocdn.net/dn/pH86g/btrH0wWOJcu/TMH3iEJRBpwUiU7DvOC5Ek/img.png' />
  
routes/hotels.js

위 사진과 같이 api endpoint 마다 에러 발생 시, response 하고싶은 http 상태코드와 오류 메세지를 입력해준다.

<img src='https://blog.kakaocdn.net/dn/bB7RtG/btrHZUjDSL0/JkRkzIWjHFHbAXne8ogKKk/img.png' />
  
response로 받는 데이터 값

그러면 위와 같이 내가 입력해둔 HTTP 상태코드와 메세지 그리고 왜 오류가 났는지에 대해 한눈에 볼 수 있게끔 보내줄 수 있다!
 
</div>
