### 01. 왜 CLI를 사용할까?
#### 1) 마우스 클릭 vs 키보드 입력
- Git은 리눅스 운영체제를 만든 리누스 토발즈(Linus torvalds)가 리눅스의 소스 관리를 위해 만들었다. 
- 처음에는 CLI 환경만 지원했으나, GitHub과 함께 Git이 유명해지면서 많은 사용자가 CLI 환경을 어려워해 GUI 프로그램이 등장하게 된다.

	- GUI 프로그램은 CLI 기능 중 자주 쓰는 기능만 모아서 만들었기 때문에 Git의 모든 기능(옵션)을 사용할 수는 없다.

#### 2) CLI 시작 전 이것만은 반드시
- CLI 명령 실행 중 발생하는 에러 메시지
- 에러 메시지는 중요하다. 꼭 메시지를 읽자.

	- 에러 발생 예시
	```
	$ git it is good day to code
	git: 'it' is not a git command. See 'git --help'.

	The most similar command is
			init
	```
		1. 'it'이라는 명령은 없으니 'git --help'를 한 번 확인해 봐라.
		2.  가장 근접한 명령은 'init'이다.

<br/>

### 02. Git Bash를 시작하자
- Git Bash는 CLI 프로그램이다.

#### 1) Git Bash 실행 및 CLI 기본 명령어 파악하기
-  프롬프트(Prompt) : CLI에서 가장 기본적인 정보를 보여준다.      
                                  ($ 기호와 윗줄에 표시된 경로 등을 합친 것을 의미.)

- 기본적으로 Git Bash를 시작하면 현재 폴더는 사용자의 홈 폴더에서 시작한다.
	```
	eunjaeui-MacBookPro:~ eunjae$
	```
	- `~`는 폴더 전체 경로를 줄여서 나타낸 것이다.

-  프롬프트 끝에 브랜치명이 보인다면 이는 Git 작업 폴더라는 의미임을 기억해 두자.
	```
	eunjaeui-MacBookPro: ~/Desktop/github/iTshirt-cat(master) $
	```
	- 현재 브랜치명인 `(master)`가 적혀있다.

- 기본적인 Git 명령어 몇 가지
- 
| 명령어 | 설명 |
|--------| -------------|
| pwd | 현재 폴더의 위치를 확인한다. |
| Is -a | 형재 폴더의 파일 목록을 확인한다. <br/> -a 옵션을 이용해 숨김 파일도 볼 수 있다. |
| cd | 홈 폴더로 이동한다. <br/> 홈 폴더는 사용자 이름과 폴더명이 길고 내 문서 폴더의 상위 폴더이다. |
| cd <폴더이름> | 특정 위치의 디렉토리로 이동한다. |
| cd ../ | 현재 폴더의 상위 폴더로 이동한다. |
| mkdir <새폴더이름> | 현재 폴더의 아래에 새로운 폴더를 만든다. |
| echo "Hello Git" | 메아리라는 뜻. <br/> 화면에 " " 안의 문장인 "Hello Git"을 표시한다. |

#### 2) Git 로컬저장소 생성하기
- 내 문서로 이동하기
	- `$ cd Documents/`
		-	Documents폴더로 이동	
	- `$ pwd`		
		- 현재 폴더의 위치 확인

- Git 로컬저장소를 위한 새 폴더 만들기
	- `eunjaeui-MacBookPro:Documents eunjae$ mkdir hello-git-cli`
		-	`hello-git-cli`라는 이름의 새로운 폴더 생성	
	- `eunjaeui-MacBookPro:Documents eunjae$ cd hello-git-cli`
		- 새로 생성한 폴더로 이동
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ pwd`
		- 현재 폴더 위치 확인
		- `/Users/eunjae/Documents/hello-git-cli`

- Git 로컬 저장소를 위해 만든 새 폴더 정보 보기
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ git status`
		- git status 명령은 Git 저장소(정확하게는 워킹트리)에서만 정상적으로 수행되는 명령이다.
		
		|   명령어            |   설명        |
		| ---------------- | ----------- |
		|   git statue      |  git status -s   Git 워킹트리의 상태를 보는 명령으로, 매우 자주 사용한다. <br/> 워킹트리가 아닌 폴더에서 실행하면 오류가 발생한다.|
		|   git status -s   | git status 명령 보다 짧게 요약해서 상태를 보여주는 명령으로, 변경된 파일이 많을 때 유용하다. |

	- Git 저장소가 아닌 위치에서 `$ git status` 명령을 수행했는데 오류가 뜨지 않는 경우.
		- 새로 만든 폴더가 git 프로젝트의 하위 폴더라는 의미. 
			- 즉, 해당 폴더의 상위 폴더 중 어떤 폴더가 Git 저장소로 이미 초기화되어 있다는 의미.
			- Git을 처음 접하는 입문자가 많이하는 실수로 대부분 내 문서(Documents) 폴더가 Git 저장소인 경우가 많다.
			- 이럴 경우 실수로 `git push`명령을 사용한다면 내 문서 내의 자료가 통채로 GitHub에 공개될 수 있다.
		- 해결방법
			- 어딘가에 생성된 `[.git]`폴더를 삭제해줘야 한다.
				- `[.git]`폴더는 숨김 처리 되어있다.
				- 숨김처리 된 폴더를 보는 방법
					- (mac) command + shift + `.`
				
- Git 저장소 초기화
	-	`eunjaeui-MacBookPro:hello-git-cli eunjae$ git init`
		-	Git 저장소 생성
		-	`Initialized empty Git repository in /Users/eunjae/Documents/hello-git-cli/.git`
		
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ ls -a`
		- 현재 폴더 내 '파일 목록' 확인
		- `.  ..  .git` (  ./ ../ .git/ )
		
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ git status`
		- 워킹 트리 상태 확인
		
				On branch master     
				
				No commits yet     
				   
				nothing to commit (create/copy files and use "git add" to track)


			|         git init | 
			| -------- |
			|        현재 폴더에 Git 저장소를 생성한다. <br/> 현재 폴더에는 [.git]이라는 숨김 폴더가 생성되는데 사실 이 폴더가 로컬저장소이다. | 

- 워킹트리 
	- 로컬저장소가 있는 현재 폴더.
	- 즉, 일반적인 작업 폴더를 의미한다.

- Git의 기본적인 용어

	|   용어   |    설명  |
	| --- | --- |
	| 워킹트리<br/>(working tree) | 워크트리, 워킹 디렉토리, 작업 디렉토리, 작업 폴더 모두 같은 뜻으로 사용된다.<br/> 일반적으로 사용자가 파일과 하위 폴더를 만들고 작업 결과물을 저장하는 곳을 Git에서는 워킹트리라고 부른다. 공식문서에서는 워킹트리를 '커밋을 체크하웃하면 생성되는 파일과 디렉토리'로 정의하고 있다. 정확하게는 작업 폴더에서 [.git]폴더(로컬저장소)를 뺀 나머지 부분이 워킹드리이다.   |
	| 로컬저장소<br/>(local repository) | Git init 명령으로 생성되는 [.git]폴더가 로컬저장소이다. 커밋, 커밋을 구성하는 객체, 스테이지가 모두 이 폴더에 저장된다. |
	| 원격저장소<br/>(remote reopsitory) | 로컬저장소를 업로드하는 곳을 원격저장소라고 한다. 우리가 사용하고 있는 GitHub 저장소가 원격저장소다.(G와 H가 대문자라는 것에 유의) |
	| Git 저장소 | Git 명령으로 관리할 수 있는 폴더 전체를 일반적으로 Git 프로젝트 혹은 Git 저장소라고 부른다. 엄밀하게는 로컬저장소를 의미하지만 넓은 의미로 작업 폴더를 의미하기도 한다.  |
	
#### 3) 옵션 설정하기
```
	$ git config --global <옵션명>
		: 지정한 전역 옵션의 내용을 살펴본다.

	$ git config --global <옵션명> <새로운값>
		: 지정한 전역 옵션의 값을 새로 설정

	$ git config --global --unset <옵션명>
		: 지정한 전역 옵션을 삭제

	$ git config --local <옵션명>
		: 지정한 지역 옵션의 내용을 살펴본다.

	$ git config --local <옵션명> <새로운값>
		: 지정한 지역 옵션의 값을 새로 설정

	$ git config --local --unset <옵션명>
		: 지정한 지역 옵션의 값을 삭제

	$ git config --system <옵션명>
		: 지정한 시스템 옵션의 내용을 살펴본다.

	$ git config --system <옵션명> <값>
		: 지정한 시스템 옵션의 값을 새로 설정

	$ git config --system --unset <옵션명> <값>
		: 지정한 시스템 옵션의 값을 삭제

	$ git config --list
		: 현재 프로젝트의 모든 옵션을 살펴본다.
```

- git config 명령으로 옵션을 보거나, 값을 바꿀 수 있다.
- Git의 옵션에는 `지역 옵션`과 `전역 옵션`, `시스템 환경 옵션` 에 종류가 있다.
	- 시스템 환경 옵션은 Git 저장소에서만 유효한 옵션.
	- 일반적으로 개인 PC에서는 전역 옵션을 사용.
	- 공용 PC나 Git을 써야할 일이 있다면 지역 옵션을 사용.
	- 우선순위는 `지역옵션 > 전역옵션 > 시스템옵션` 순.
<br/>

- Git 전역 옵션 설정
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ git config --global user.name`

		- `EunJaePark` 이라는 결과가 나타났다.
			- 현재 설정 된 값이 `EunJaePark`으로 있다는 의미.
			- 만약, 아무런 결과도 출력되지 않는다면 현재 설정된 값이 없다는 의미로, 바로 새로운 값을 설정하면 된다.
			- ex) `$ git config --global user.name "새로운 이름"`

- CLI를 사용하면 텍스트 에디터를 쓸 일이 생긴다. 현재 Git Bash의 기본 에디터는 보통 리눅스 운영체제에서 주로 쓰는 vim이나 nano로 설정되어 있다. vim이 뭔지 모를 경우, 기본 에디터를 Visual Studio Code로 변경하는 것이 좋다.
- Git 기본 에디터 확인
	- ```$ git config core.editor```
	- ```$ git config --global core.editor```
	- ```$ git config --system core.editor```
- Git의 기본 에디터를 VSCode로 설정해주자.
	- [해당 블로그 참고](https://medium.com/@hohpark/vs-code%EB%A5%BC-git-diff-tool%EB%A1%9C-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0-88baa1d9f2b3)

<br/>

### 03. 기본 CLI 명령어 살펴보기
#### 1) 스테이징과 커밋을 수행하는 add, commit
- 기본적인 git 명령들
	```
	 $ git add 파일1 파일2 ...
		: 파일들을 스테이지에 추가.
		  새로 생성한 파일을 스테이지에 추가하고 싶다면 반드시 add 명령어를 사용한다.

	 $ git commit
		: 스테이지에 있는 파일들을 커밋.

	 $ git commit -a
		: add 명령을 생략하고 바로 커밋하고 싶을 때 사용.
		  변경된 파일과 삭제된 파일은 자동으로 스테이징되고 커밋된다.
		  주의할 점은 untracked 파일은 커밋되지 않는 다는 것.

	 $ git push [-u] [원격저장소별명] [브랜치이름]
		: 현재 브랜치에서 새로 생성한 커밋들을 원격저장소에 업로드한다.
		  -u 옵션으로 브랜치의 업스트림을 등록할 수 있다.
		  한 번 등록한 후에는 git push만 입력해도 된다.

	 $ git pull
		: 원격저장소의 변경사항을 워킹트리에 반영.
		  사실은 git fetch + git merge 명령이다.

	 $ git fetch [원격저장소별명] [브랜치이름]
		: 원격저장소의 브랜치와 커밋들을 로컬저장소와 동기화.
		  옵션을 생략하면 모든 원격저장소에서 모든 브랜치를 가져온다.

	 $ git merge 브랜치이름
		: 저장한 브랜치의 커밋들을 현재 브랜치 및 워킹트리에 반영. 
	```
<br/>

- 간단한 텍스트 파일을 생성하고 확인하기
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ echo "hello git"`
		- 화면에 " " 안의 텍스트를 보여준다. 
		- `hello git`

	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ echo "hello git" > file1.txt`
		- " " 안의 텍스트로 file1.txt 파일 생성

	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ ls`
		- 현재 폴더의 파일 목록 확인.
		- `file1.txt` : 방금 생성한 파일이 존재함을 나타내 준다.

	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ git status`
		- 상태를 살펴봄.
			```
			On branch master

			No commits yet

			Untracked files:

			(use "git add <file>..." to include in what will be committed)

					file1.txt

			nothing added to commit but untracked files present (use "git add" to track)
			```	
		- file1.txt라는 파일이 생성되었고, untracked상태임을 확인할 수 있다.

- 생성한 파일(변경 내용)을 스테이지에 추가하기
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ git add file1.txt`
	
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ git status`
		- 상태를 확인하면 아래와 같은 결과가 나타남.
			```
			On branch master

			No commits yet

			Changes to be committed:
			(use "git rm --cached <file>..." to unstage)

			new file: file1.txt
			```
			- 새로 만든 file1.txt 파일이 스테이지 영역에 추가된 것을 확인할 수 있다.

#### 2) reset 명령으로 스테이징 취소하기
- 위에 보이는 `"git rm --cached <file>..."` 명령으로 스테이지에서 내릴 수 있지만, 더 자주 사용하는 명령이 있다.
- ` $ git reset [파일명]`
	- 스테이지 영역에 있는 파일들을 스테이지에서 내린다(언스테이징).
	- 워킹트리의 내용은 변경되지 않는다. 옵션을 생략할 경우 스테이지의 모든 변경사항을 초기화한다.
	- reset의 3가지 옵션
		- soft, mixed, hard
		- 옵션 없이 사용하면 기본적으로 mixed reset으로 동작한다.

- 스테이지에서 파일 언스테이징하기
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ git reset file1.txt`
		- file1.txt 파일 언스테이징 (위에서 스테이지에 올려줬던 파일 다시 내림).

	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ git status`
		- 상태 확인.
			```
			On branch master

			No commits yet

			Untracked files:
				(use "git add <file>..." to include in what will be committed)

					file1.txt
					
			nothing added to commit but untracked files present (use "git add" to track)
			```
			- file1.txt 파일이 언스테이징되어 스테이지에서 내려간 상태임을 확인할 수 있다.
			
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ ls`
		- 현재 폴더의 파일 목록을 확인
		- `file1.txt`

	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ cat file1.txt`
		- cat 명령으로 파일 내용이 변경되었는지 확인
		- `hello git`


#### 3) CLI로 첫 번째 커밋 생성
- 앞에서 언스테이징을 했으므로 다시 git add 명령을 실행 후 커밋한다. 커밋은 git commit 명령으로 수행한다.

- 첫 번째 CLI 커밋
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ git add file1.txt`
		- add를 이용해 스테이지에 추가

	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ git status`
		- 상태 확인
		- file1.txt가 스테이징 된 것을 확인.
			```
			On branch master

			No commits yet

			Changes to be committed:
				(use "git rm --cached <file>..." to unstage)

					new file: file1.txt
			```
  
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ git commit`
		- commit 명령어를 입력하면 VSCode가 열린다.
			- 앞서 기본 에디터를 VSCode로 설정해 뒀기 때문.
		- VScode에서 커밋 메시지를 작성 후 저장하고 VSCode를 닫는다.
			- VSCode에서 커밋 메시지를 작성할 때, 첫 줄과 둘째 줄 사이는 반드시 한 줄 비워줘야한다.
			- 첫 줄에는 작업 내용 요약(제목), 둘째 줄에는 자세하게 작업 내용을 기록(본문).
		- 아래처럼 터미널에 커밋메시지와 커밋되었다는 문구가 나타난다.
			```
			[master (root-commit) 67352a2] 첫 번째 커밋

			1 file changed, 1 insertion(+)

			create mode 100644 file1.txt
			```
		- 만약 git commit 명령 실행 후, 커밋을 하고싶지 않다면 VSCode에서 아무것도 추가하지 않고 종료해주면 된다.

#### 4) CLI로 log 살펴보기
- git log 명령으로 git의 커밋 히스토리 확인해 보기
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ git status`
		- 상태 확인
			```
			On branch master
			nothing to commit, working tree clean
			```
			
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ git log --oneline --graph --all --decorate`
		- 커밋 히스토리 확인
		- '첫 번째 커밋'이라는 메시지로 커밋했던 히스토리가 보인다.
			
			`* 67352a2 (**HEAD ->** **master**) 첫 번째 커밋`
			- 커밋 히스토리에 보이는 앞의 16진수 7자리 숫자는 커밋 체크섬 혹은 커밋 아이디이다.
			- 실제로 커밋 체크섬은 40자리인데 앞의 7자리만 화면에 보여진다.
			- SHA1해시 체크섬 값을 사용하는 것으로, 전 세계에서 유일한 값을 가진다. (모든 커밋의 아이디가 다르다는 말)

- git log의 다양한 옵션
	```
	 $ git log
		 : 현재 브랜치의 커밋 이력을 보는 명령

	 $ git log -n<숫자>
		 : 전체 커밋 중에서 최신 n개의 커밋만 살펴봄.
		   아래의 다양한 옵션과 조합해서 쓸 수 있다.

	 $ git log --oneline --graph --decorate --all
		 : 자주 사용하는 옵션으로 간결하고 멋지게 보여준다.
		   (소스트리로 보는 것이 더 보기 좋다)

			--oneline
				: 커밋 세지시를 한 줄로 요약해서 보여줌.
				  생략하면 커밋 정보를 자세히 표시.
			
			--graph
				: 커밋 옆에 브랜치의 흐름을 그래프로 보여줌.
				 GUI와 유사한 모습으로 나온다.
				 
			--decorate
				: 원래는 -decorate=short 옵션을 의미.
				  브랜치와 태그 등의 참조를 간결히 표시.
				  
			--all
				: all 옵션이 없을 경우 HEAD와 관계없는 옵션은 보여주지 않는다.
	```
	
	- 각각의 옵션의 조합에 따라 결과가 달라진다.
		```
		 $ git log
			: HEAD와 관련된 커밋들이 자세하게 나온다.

		 $ git log --oneline
			 : 간단히 커밋 해시와 제목만 보고 싶을 때

		 $ git log --oneline --graph --decorate
			 : HEAD와 관련된 커밋들을 조금 터 자세히 보고 싶을 때

		 $ git log --oneline --graph --all --decorate
			 : 모든 브랜치들을 보고 싶을 때

		 $ git log --oneline -n5	
			 : 내 브랜치의 최신 커밋을 5개만 보고 싶을 때
		```

- 좋은 커밋 메시지의 7가지 규칙
	1. 제목과 본문을 빈 줄로 분리한다.
	2. 제목은 50자 이내로 쓴다.
	3. 제목을 영어로 쓸 경우 첫 글자는 대문자로 쓴다.
	4. 제목에는 마침표를 넣지 않는다.
	5. 제목을 영어로 쓸 경우 동사원형(현재형)으로 시작한다.
	6. 본문을 72자 단위로 줄바꿈한다.
	7. 어떻게 보다 무엇과 왜를 설명한다.

#### 5) 도움말 기능 사용하기
- Git에는 각 명령의 도움말을 볼 수 있는 명령이 있다.
- `$ git help <명령어>` 
	- 해당 명령어의 도움말을 표시
	- 도움말에는 명려으이 의미와 세부적인 옵션들이 매우 자세하게 표시된다.

- git 도움말 사용해 보기
	- `$ git help status` 
	- `$ git help commit`
	- `$ git help add`

- $ git help ~ 를 사용 후 빠져나오려면 ```q```자판을 눌러주면 된다.

<br/>

### 04. 원격저장소 관련 CLI 명령어
#### 1) remote, push, pull
- 커밋을 했으니 원격저장소에 push를 보내야 한다.
- `$ git remote add <원격저장소 이름> <원격저장소 주소>`
	- 원격저장소 등록.
	- 원격저장소는 여러 개 등록할 수 있지만 같은 별명의 원격저장소는 하나만 가질 수 있다. 통상 첫 번째 원격저장소를 origin으로 지정한다.
	
- `$ git remote -v`
	- 원격저장소 목록을 살펴본다.
	
- 원격저장소 등록 및 push
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ git remote add origin https://github.com/EunJaePark/hello-git-cli.git`
		- 새로 생성한 원격저장소 등록.
		
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ git remote -v`
		- 원격저장소 목록을 살펴 봄
			```
			origin  https://github.com/EunJaePark/hello-git-cli.git (fetch)
			origin  https://github.com/EunJaePark/hello-git-cli.git (push)
			```
	- push해줌 
	`eunjaeui-MacBookPro:hello-git-cli eunjae$ git push```
		- 실패했다는 에러 메시지 나옴.
			```
			fatal: The current branch master has no upstream branch.
			To push the current branch and set the remote as upstream, use

				git push --set-upstream origin master
			```
			- 로컬저장소의 [master] 브랜치와 연결된 원격저장소의 브랜치가 없어서 발생한 오류이다.
			- upstream 브랜치는 로컬저장소와 연결된 원격저장소를 일컫는 단어이다.
			- 에러메시지에서 알려준 대로 `--set-upstream`을 쓰거나 이 명령의 단축 명령인 `-u` 옵션을 사용한다.
			- 이후에는 origin 저장소의 [master]브랜치가 로컬저장소의 [master] 브랜치의 업스트림으로 지정되어 `git push `명령어만으로도 에러 없이 push가 가능해진다.
			- 참고로 Git Bash에서 긴 명령은 `--`(대시 두 개)로, 짧은 명령은 `-`(대시 한 개)로 시작하는 경우가 많다.

- git push 재시도
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ git push -u origin master`
		- push와 동시에 업스트림 지정
			```
			Enumerating objects: 3, done.
			Counting objects: 100% (3/3), done.
			Writing objects: 100% (3/3), 302 bytes | 302.00 KiB/s, done.
			Total 3 (delta 0), reused 0 (delta 0)
			To https://github.com/EunJaePark/hello-git-cli.git
			* [new branch]  master -> master
			Branch 'master' set up to track remote branch 'master' from 'origin'.
			```

	-	`eunjaeui-MacBookPro:hello-git-cli eunjae$ git log --oneline -n1`
		-	브랜치의 최신 커밋 1개만 확인
			```
			b6e1657 (**HEAD ->** **master**, **origin/master**) 첫 번째 커밋
			```
			
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ git push`
		- 다시 push 해 줌
		- `Everything up-to-date`

	- 이전 GUI실습 때 내 컴퓨터의 keychain을 새로 생성한 두 번째 GitHub계정으로 바꿔놔서 push재시도에서 헤맸다.
		- 다시 keychain을 기존 깃헙 계정으로 수정해주니까 push 재시도 성공했다.
		- 폴더, 파일, 원격저장소 생성 다시 처음부터 해보았는데도 실패해서 좌절했었음.....ㅠ....
- `eunjaeui-MacBookPro:hello-git-cli eunjae$ git log`
	- git log 명령을 통해 확인.
		```
		commit b6e1657dcdcee7babe501dfecf9e4d84058d27e7 (**HEAD ->** **master**, **origin/master**)

		Author: EunJaePark <design0728@naver.com>

		Date: Mon Jun 22 14:34:31 2020 +0900

		  

		첫 번째 커밋

		간단하게 hello git이라고 쓴 내용을 커밋했다.
		```
		- HEAD는 [master]를 가르키고 있고, [origin/master]브랜치도 생겨난 것을 볼 수 있다.
		- HEAD가 가리키는 [master]는 로컬의 [master]브랜치이고, [origin/master]는 원격저장소인 GitHub의 마스터 브랜치이다.

#### 2) clone
- CLI로 clone을 해보자.
- `$ git clone` 명령을 사용할 때, 저장소 주소가 꼭 원격일 필요는 없다. 때에 따라 로컬저장소를 클론으로 복제하면 편리하게 사용할 수 있다.

- git clone 사용해 보기
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ pwd`
		- 현재 위치 확인			
			`/Users/eunjae/Documents/hello-git-cli`
		
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ cd ../`
		- 상위 디렉토리로 이동!

	- `eunjaeui-MacBookPro:Documents eunjae$ git clone https://github.com/EunJaePark/hello-git-cli.git`
		- 원격저장소를 clone으로 복제 시도
			```
			fatal: destination path 'hello-git-cli' already exists and is not an empty directory.
			```
			- 실패. 
			- [새로운 폴더명] 옵션을 지정하지 않으면 복제한 프로젝트 이름과 같은 폴더를 만들게 되는데, 이미 [hello-git-cli]라는 폴더가 있기 때문에 실패한 것.

- git clone으로 로컬저장소 복제하기([새로운 폴더명] 옵션 사용)
	- `eunjaeui-MacBookPro:Documents eunjae$ git clone https://github.com/EunJaePark/hello-git-cli.git hello-git-cli2`
		- 새로운 폴더명  `hello-git-cli2`를 설정해 클론
			```
			Cloning into 'hello-git-cli2'...
			remote: Enumerating objects: 3, done.
			remote: Counting objects: 100% (3/3), done.
			remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
			Unpacking objects: 100% (3/3), done.
			```
	- `eunjaeui-MacBookPro:Documents eunjae$ ls`
		- Documents에 들어있는 폴더 확인
			```
			hello-git-cli
			hello-git-cli2
			movie
			터미널에서 저장된 출력
			```
	- `eunjaeui-MacBookPro:Documents eunjae$ cd hello-git-cli2`
		- 클론한 폴더로 위치 이동

	- `eunjaeui-MacBookPro:hello-git-cli2 eunjae$ git log --oneline`
		- 간단한 커밋 정보 확인
			```
			b6e1657 (**HEAD ->** **master**, **origin/master**, **origin/HEAD**) 첫 번째 커밋
			```
	- `eunjaeui-MacBookPro:hello-git-cli2 eunjae$ git remote -v`
		- 원격저장소 목록 확인
			```
			origin  https://github.com/EunJaePark/hello-git-cli.git (fetch)

			origin  https://github.com/EunJaePark/hello-git-cli.git (push)
			```

- 추가 commit and push(클론한 저장소에서 커밋해보기)
	- `eunjaeui-MacBookPro:hello-git-cli2 eunjae$ echo "second" >> file1.txt`
		- file1.txt 파일에 'second'라는 내용 추가

	- `eunjaeui-MacBookPro:hello-git-cli2 eunjae$ cat file1.txt`
		- file1.txt파일의 내용 확인
			```
			hello git

			second
			```
	- `eunjaeui-MacBookPro:hello-git-cli2 eunjae$ git commit -a`
		- 스테이징 없이 바로 커밋
			```
			[master 2ec7e32] 두 번째 커밋

			1 file changed, 1 insertion(+)
			```
	- `eunjaeui-MacBookPro:hello-git-cli2 eunjae$ git push`
		- 수정한 파일 push
			```
			Enumerating objects: 5, done.
			Counting objects: 100% (5/5), done.
			Writing objects: 100% (3/3), 286 bytes | 286.00 KiB/s, done.
			Total 3 (delta 0), reused 0 (delta 0)
			To https://github.com/EunJaePark/hello-git-cli.git
				b6e1657..2ec7e32  master -> master
			```
	- `eunjaeui-MacBookPro:hello-git-cli2 eunjae$ git log --oneline`
		- 커밋 정보 간단하게 확인
			```
			2ec7e32 (**HEAD ->** **master**, **origin/master**, **origin/HEAD**) 두 번째 커밋

			b6e1657 첫 번째 커밋
			```

<br/>

- 다시 첫 번째 저장소로 돌아가서 두 번째 저장소에서 변경한 내용을 내려받아보자. ( `git pull `)
	- ` eunjaeui-MacBookPro:hello-git-cli2 eunjae$ cd ~/Documents/hello-git-cli`
		- 처음 저장소로 이동
				
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ git log --oneline`
		- 결과를 보면 기존에 커밋한 첫 번째 커밋만 있음을 알 수 있다.
			```
			b6e1657 (**HEAD ->** **master**, **origin/master**) 첫 번째 커밋
			```
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ git pull`
		- 두 번째 저장소의 변경사항을 내려받음
			```
			remote: Enumerating objects: 5, done.
			remote: Counting objects: 100% (5/5), done.
			remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
			Unpacking objects: 100% (3/3), done.
			From https://github.com/EunJaePark/hello-git-cli
				b6e1657..2ec7e32  master -> origin/master
			Updating b6e1657..2ec7e32
			Fast-forward
				file1.txt | 1 +
				1 file changed, 1 insertion(+)
			```
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ git log --oneline`
		- 커밋을 다시 확인해보면 두 번째 저장소에서 커밋한 내용이 추가되었음을 보여준다.
			```
			2ec7e32 (**HEAD ->** **master**, **origin/master**) 두 번째 커밋
			b6e1657 첫 번째 커밋
			```
	- `eunjaeui-MacBookPro:hello-git-cli eunjae$ cat file1.txt`
		- file1.txt의 내용을 확인해 보면 수정된 내용이 추가된 것을 볼 수 있다.
			```
			hello git
			second
			```
			
<br/>

- 처음 생성했던 Git 저장소로 이동한 후 git pull 명령을 수행했다. `pull`이란 `fetch`와 `merge`를 합친 것이라고 보면 된다.

