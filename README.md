# manual-web

### nodejs

### 서브라임 텍스트 sublime text
스니펫 :  
https://packagecontrol.io/browse/labels/snippets  


### Material design layout
학습 :  
https://www.tutorialspoint.com/materialdesignlite/index.htm  

https://getmdl.io/index.html    

아이콘 :
<h3><i class="material-icons">build</i> 관리자 페이지 : 앱 서비스</h3>  
https://material.io/tools/icons/?style=baseline  

### 파이어베이스 파이어스토어 자바스크립트 쿼리 firebase firestore javascript query

customers의 userNickname과 일치하는 documnet의 key값을 받아서  
points 컬렉션을 조회하는 내용. 더불어 doc()의 필드값을 업데이트 함  
```
Collection : customers
                 doc()
                        timestamp :
                        currentPoint :
                        userNickname :
                        userMail : 
                             Collection : points
                                            doc()
                                               point :
                                               timestamp :
```
```
// Saves a new message on the Firebase DB.
function savePoint(userText, pointText) {
  // 1. 사용자의 userNickname을 찾아서 uid값을 가져온다
  // 2. 사용자 uid에 대한 point collection에 값을 집어넣는다

  // Create a reference to the cities collection
  var customerRef = firebase.firestore().collection('customers');

  // Create a query against the collection.
  var query = customerRef.where("userNickname", "==", userText);

  var inputValue = parseInt(pointText);

  // 사용자 닉네임과 일치하는 쿼리를 진행한다.
  query
    .get()
    .then(function (querySnapshot) {

      querySnapshot.forEach(function (doc) {
        // doc.data() is never undefined for query doc snapshots
        console.log(doc.id, " => ", doc.data());

        // 문서의 key값과 점수를 받는다.
        var documentKey = doc.id;
        var documentValue = parseInt(doc.data().recentPoint);

        // 저장된 값보다 입력된값이 크면, 변경 아니면 변경하지않음
        if (inputValue > documentValue) {

          // Set the "capital" field of the city 'DC'
          return customerRef.doc(documentKey).update({
            recentPoint: inputValue
          })
            .then(function () {
              console.log("Document successfully updated!");
              console.log("사용자의 최고점수가 갱신됩니다.");
            })
            .catch(function (error) {
              // The document probably doesn't exist.
              console.error("Error updating document: ", error);
              alert("업데이트에 에러가 발생했습니다!");
            });
            
        }

        var pointRef = customerRef.doc(documentKey).collection('points');

        return pointRef.add({
          point: inputValue,
          timestamp: firebase.firestore.FieldValue.serverTimestamp()
        })
        .then(function(){
          console.log("Document successfully updated!");
          alert("점수를 기재합니다.");

        })
        .catch(function (error) {
          console.error('Error writing new message to Firebase Database', error);
          alert("업데이트에 에러가 발생했습니다!");
        });
      });
    })
    .catch(function (error) {
      console.log("Error getting documents: ", error);
      alert("업데이트에 에러가 발생했습니다!");
    });

  resetMaterialTextfield(messageInputUserElement);
  resetMaterialTextfield(messageInputPointElement);
  togglePointButton();

}
```

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

firebase deploy --except functions (배포)

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
