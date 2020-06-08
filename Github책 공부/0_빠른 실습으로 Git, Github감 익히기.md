<h3>01. Git, 그리고 Github</h3>

- git : 버전 관리 시스템(버전관리(=내가 원하는 버전으로 이동할 수 있게 해주는 것)를 도와주는 툴).
- github : git으로 관리하는 프로젝트를 올려둘 수 있는 git호스팅 사이트.
           (git호스팅 사이트는 github외에도 GitLab, BigBucket 등 다양하다)
- 오픈소스 : 누구든지 기여할 수 있는 공개저장소 프로젝트.



<br/>
<h3>02. Git을 설치하고 로컬저장소에서 커밋 관리하기</h3>

<h4> 1) 로컬저장소 생성</h4>

- [iTshirt-cat]폴더 생성 후, TextEdit에서 READEME 파일하나 생성.
- 터미널에서 해당 폴더로 이동 후 ```$ git init```해서 [.git]폴더 생성.
- [.git]폴더에는 Git으로 생성한 버전의 정보들과 원격저장소의 주소 등이 들어있다.

  [.git]폴더를 로컬 저장소라고 부른다.

- 정리하자면, 일반 프로젝트 폴더에 'git init'(=git 초기화 과정)명령어를 통해 로컬저장소를 만들면 그때부터 이 폴더에서 버전관리를 할 수 있는 것이다.


<h4> 2) 첫 번째 커밋 만들기</h4>

- README파일을 하나의 버전으로 만들어보자.

  이렇게 생성된 각 버전을 Git에서는 ```커밋```이라고 한다.
  
- 버전 관리를 위해 내 정보를 등록해야 한다.
   ```
   $ git config --global user.email "이메일주소@이메일주소.이메일"
   $ git config --global user.name "이름"
   ```
- 그 다음, 커밋할 파일을 추가한 뒤, 커밋 명령어를 입력한다.(커밋 메세지도 함께 입력할 수 있다.)
   ```
   $ git add 파일명.확장자
   $ git commit -m "커밋 메세지"
   ```
   - ```-m```은 'message'의 약자이다.
- ```1 file changed, 1 insertion(+)``` : 이 메세지가 터미널에 뜨면 성공한 것이다.
- 커밋한 파일을 수정하고 다시 커밋할 경우 아래의 메세지가 보이면 성공이다.(새로운 버전을 생성한 것.)

   ``` 1 file changed, 1 insertion(+), 1 deletion(-)```


<h4> 3) 다른 커밋으로 시간 여행하기</h4>

- 이전 커밋부터 다시 개발하고 싶을 경우 Git을 이용해 이전 커밋으로 되돌아 갈 수 있다.
- ```$ git log```명령어로 지금까지 만든 커밋들을 확인하면,
   
   아래와 같이 지금까지 생성한 커밋들의 정보가 터미널에 나타난다.
   
   ```
   eunjaeui-MacBookPro:iTshirt-cat eunjae$ git log
   commit ba7c4088aec48ab64791cbf42c83806ba873fa4f (HEAD -> master)
   Author: EunJaePark <design0728@naver.com>
   Date:   Mon Jun 8 11:35:54 2020 +0900

       설명 업데이트

   commit a84ac9ff6b143d0eb95c11aa076bc7cb7b52e2fb
   Author: EunJaePark <design0728@naver.com>
   Date:   Mon Jun 8 11:34:02 2020 +0900

       사이트 설명 추가
   eunjaeui-MacBookPro:iTshirt-cat eunjae$ 
   ```
- 되돌리려는 커밋의 앞 7자리 커밋 아이디를 복사해서 ```$ git checkout 커밋아이디```를 입력해준다. (커밋 아이디 전체를 입력해도 된다.)

   - ex) ```$ git checkout a84ac9f```를 입력 후, 
         ```HEAD is now at a84ac9f 사이트 설명 추가```라는 글이 나타나면 성공한 것이다.

- 최신 커밋으로 이동하려면 최신 커밋의 아이디를 입력해도 되지만,

   간단하게 ```-```를 이용해서 ```$ git checkout -```를 입력해도된다.

- 이처럼 원하는 커밋으로 이동하는 것을 '체크아웃 한다'라고 표현한다.



<br/>
<h3>03. GitHub 원격저장소에 커밋 올리기</h3>

- 다른 개발자와 함께 버전을 관리하고 싶다면 원격저장소에 올려야 한다. 

<h4> 1) 원격저장소 만들기 </h4>

- 원격저장소 
    - GitHub 웹 사이트에 프로젝트를 위한 공용 폴더를 만든다고 보면 된다.
    - 로컬저장소와 구분하는 개념으로 원격저장소라고 한다.
<br/>

- [New repository]를 생성해준다.
   
  - ex) iTshirt라는 new repository를 생성해주면 ```https://github.com/EunJaePark/iTshirt.git```라는 주소를 가진 원격저장소가 생성된다.

- 생성된 주소를 통해 원격저장소에 접속할 수 있다.
- ```$ git remote add origin 원격저장소주소```를 입력해서 로컬저장소에 원격저장소의 주소를 알려준다.

   - ex) ```$ git remote add origin https://github.com/EunJaePark/iTshirt.git```

- ```$ git push origin master```를 입력해서 로컬저장소에 있는 커밋들을 원격저장소에 push해주면 된다.

   - 로그인이 되어있지 않은 상태면 GitHub 로그인 창이 뜬다. 로그인을 해주면 된다.
   
- 100% 완료되었다는 ```100% (1/1), done.```문구가 보이면 성공한 것이다.
<br/>

+ 생성했던 repository 삭제 후 재생성 했을 때 ```fatal: remote origin already exists.```라는 에러가 발생했다.

  이럴 경우, ```$ git remote rm origin```또는 ```$ git remote remove origin```를 입력해서 기존 원격저장소 연결을 삭제 후 다시 연결해주면 된다.



<br/>
<h3>04. GitHub 원격저장소의 커밋을 로컬저장소에 내려받기</h3>

- 다른 개발자가 올린 커밋을 내 컴퓨터에 받아오는 것이다.

<h4> 1) 원격저장소의 커밋을 로컬저장소에 내려받기 </h4>

- 원격저장소의 코드와 버전 전체를 내 컴퓨터로 내려받는 것을 '클론(clone)'이라고 한다.
- 빈 파일을 만들어서 위에서 만들었던 커밋을 받아와보자.
 
  ex) [iTshirt-oct]폴더 생성하고, 터미널에서 새로 생성한 파일인 [iTshirt-oct]로 경로를 변경해주자.( ```$ cd 생성한 파일경로```)
  
- 기존 iTshirt-cat 커밋의 주소를 복사한다.
   - GitHub에서 우측의 [Clonde or download]버튼 클릭해서 복사.
   - [Clonde or download]에서 [Download ZIP]을 할 경우 소스코드를 똑같이 받을 수 있지만, 원격저장소와 버전 정보를 받아올 수 없다.
   
- ```$ git clone 원격저장소 주소 .```
   - git clone 명령어 뒤에 원격저장소 주소를 적고, 한 칸 띄어서 ```.```(마침표)를 찍어준다.
   
- [iTshirt-oct] 폴더 속에 [iTshirt-cat]에 있던 README파일과 [.git]폴더(로컬저장소-숨겨진폴더)가 생성되면 성공이다. 
- 만약 ```$ git clone 원격저장소 주소 .```에서 마지막에 ```.```(마침표)를 입력하지 않을 경우, 

  [iTshirt-oct](새로 생성한 폴더) 속에 [iTshirt](다운받는 커밋)폴더가 새로 생성되고 그 안에 README파일과 [.git]폴더가 생겨 폴더 구조가 복잡해진다.

- 새로 생성한 클론 폴더([iTshirt-oct])에서 README파일을 수정하고 ```$ git add 파일명```, ```$ git commit -m "메세지"```를 해주면

  push한 커밋이 GitHub의 원격저장소(iTshirt)에 올라가 있는 것을 확인할 수 있다.
  

<h4> 2) 원격저장소의 새로운 커밋을 로컬저장소에 갱신하기 </h4>

- [iTshirt-oct](새로 생성한 폴더)에서 갱신한 README파일의 내용이 [iTshirt-cat](제일 처음 폴더)의 README파일에는 적용되지 않은 상태이다.

  따라서 [iTshirt-oct]폴더에서 원격저장소에 올린 새로운 커밋을 [iTshirt-cat]로컬저장소에 내려받아 현재 상태를 갱신해야 한다.
  
- 터미널에서 [iTshirt-cat]로컬저장소로 경로를 변경 후, ```$ git pull origin master```를 입력해준다.
   - ```pull```은 원격저장소에 새로운 커밋이 있을 경우 그 커밋을 내 로컬저장소로 받아오라는 명령어이다.
- ```1 file changed,```라는 메세지가 보이면 성공이다.

<br/>
<hr/>

<h3> ✍ < CHAPTER 0. 빠른 실습으로 Git, Github감 익히기 > 요약  </h3>

- Git : 버전 관리 시스템
- GitHub : Git으로 관리하는 프로젝트를 올려둘 수 있는 사이트
- GUI : 그래픽 유저 인터페이스. 마우스로 클릭해서 이동하는 방식
- CLI : 커맨드 라인 인터페이스. 명령어를 하나씩 입력하는 방식
- Git Bash : CLI 방식으로 Git을 사용할 수 있는 환경
- 커밋 : 버전 관리를 통해 생성된 파일, 혹은 그 행위
- log 명령어 : 지금까지 만든 모든 커밋을 확인하는 명령어
- 체크아웃한다 : checkout으로 원하는 지점으로 파일을 되돌린다는 의미
- 로컬저장소 : Git으로 버전 관리하는 내 컴퓨터 안의 폴더
- 원격저장소 : GitHub에서 협업하는 공간(폴더)
- repository(레포지토리) : 원격저장소를 의미
- push : 로컬저장소의 커밋(버전 관리한 파일)을 원격저장소에 올리는 것
- pull : 원격저장소의 커밋을 로컬저장소에 내려받는 것




