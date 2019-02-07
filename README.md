# manual-web

### nodejs

### 서브라임 텍스트 sublime text
스니펫 :  
https://packagecontrol.io/browse/labels/snippets  


### 파이어베이스 코드랩 firebase code lab

보안규칙 : 
```
service cloud.firestore {
  match /databases/{database}/documents {
    // Messages:
    //   - Anyone can read.
    //   - Authenticated users can add and edit messages.
    //   - Validation: Check name is same as auth token and text length below 300 char or that imageUrl is a URL.
    //   - Deletes are not allowed.
    match /messages/{messageId} {
      allow read;
      allow create, update: if request.auth != null
                    && request.resource.data.name == request.auth.token.name
                    && (request.resource.data.text is string
                      && request.resource.data.text.size() <= 300
                      || request.resource.data.imageUrl is string
                      && request.resource.data.imageUrl.matches('https?://.*'));
      allow delete: if false;
    }
    // FCM Tokens:
    //   - Anyone can write their token.
    //   - Reading list of tokens is not allowed.
    match /fcmTokens/{token} {
      allow read: if false;
      allow write;
    }
  }
}
```

파이어베이스 코드랩 주소 :  
https://codelabs.developers.google.com/codelabs/firebase-web/?authuser=0#0  

명령프롬프트 창 :  
npm -g install firebase-tools  
firebase --version ( 4.x 이상 확인)  
firebase login (web에서 로그인하게됨, 구글 아이디 패스워드)  
firebase use --add (파일들 있는 로컬경로 들어가서, 예 : web-start, 생성한 파베 프로젝트 선택)  
firebase serve --only hosting (파일들 있는 로컬경로 들어가서, 예 : web-start)  

import in index.html :   
<script src="/__/firebase/5.7.3/firebase-app.js"></script>  
<script src="/__/firebase/5.7.3/firebase-auth.js"></script>  
<script src="/__/firebase/5.7.3/firebase-storage.js"></script>  
<script src="/__/firebase/5.7.3/firebase-messaging.js"></script>  
<script src="/__/firebase/5.7.3/firebase-firestore.js"></script>  
<script src="/__/firebase/init.js"></script>  

npm 설치 안될떄 :  
https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally  

<center><img src="/1.png"></center>
```
<b>굵게</b>  
<strong>굵게</strong>  
<i>이탤릭</i>  
<u>밑줄</u>  
<ins>밑줄</ins>  
<tt>타자</tt>  
<sup>위첨자</sup>  
<sub>아래첨자</sub>  
<s>가로선</s>  
<del>가로선</del>  
<small>한단계 작게</small>  
<big>한단계 크게</big>  
 ```
