---


---

<h3 id="왜-cli를-사용할까">01. 왜 CLI를 사용할까?</h3>
<h4 id="마우스-클릭-vs-키보드-입력">1) 마우스 클릭 vs 키보드 입력</h4>
<ul>
<li>
<p>Git은 리눅스 운영체제를 만든 리누스 토발즈(Linus torvalds)가 리눅스의 소스 관리를 위해 만들었다.</p>
</li>
<li>
<p>처음에는 CLI 환경만 지원했으나, GitHub과 함께 Git이 유명해지면서 많은 사용자가 CLI 환경을 어려워해 GUI 프로그램이 등장하게 된다.</p>
<ul>
<li>GUI 프로그램은 CLI 기능 중 자주 쓰는 기능만 모아서 만들었기 때문에 Git의 모든 기능(옵션)을 사용할 수는 없다.</li>
</ul>
</li>
</ul>
<h4 id="cli-시작-전-이것만은-반드시">2) CLI 시작 전 이것만은 반드시</h4>
<ul>
<li>
<p>CLI 명령 실행 중 발생하는 에러 메시지</p>
</li>
<li>
<p>에러 메시지는 중요하다. 꼭 메시지를 읽자.</p>
<ul>
<li>에러 발생 예시</li>
</ul>
<pre><code>$ git it is good day to code
git: 'it' is not a git command. See 'git --help'.

The most similar command is
		init
</code></pre>
<pre><code>  1. 'it'이라는 명령은 없으니 'git --help'를 한 번 확인해 봐라.
  2.  가장 근접한 명령은 'init'이다.
</code></pre>
</li>
</ul>
<br>
<h3 id="git-bash를-시작하자">02. Git Bash를 시작하자</h3>
<ul>
<li>Git Bash는 CLI 프로그램이다.</li>
</ul>
<h4 id="git-bash-실행-및-cli-기본-명령어-파악하기">1) Git Bash 실행 및 CLI 기본 명령어 파악하기</h4>
<ul>
<li>
<p>프롬프트(Prompt) : CLI에서 가장 기본적인 정보를 보여준다.<br>
($ 기호와 윗줄에 표시된 경로 등을 합친 것을 의미.)</p>
</li>
<li>
<p>기본적으로 Git Bash를 시작하면 현재 폴더는 사용자의 홈 폴더에서 시작한다.</p>
<pre><code>eunjaeui-MacBookPro:~ eunjae$
</code></pre>
<ul>
<li><code>~</code>는 폴더 전체 경로를 줄여서 나타낸 것이다.</li>
</ul>
</li>
<li>
<p>프롬프트 끝에 브랜치명이 보인다면 이는 Git 작업 폴더라는 의미임을 기억해 두자.</p>
<pre><code>eunjaeui-MacBookPro: ~/Desktop/github/iTshirt-cat(master) $
</code></pre>
<ul>
<li>현재 브랜치명인 <code>(master)</code>가 적혀있다.</li>
</ul>
</li>
<li>
<p>기본적인 Git 명령어 몇 가지</p>
</li>
<li></li>
</ul>

<table>
<thead>
<tr>
<th>명령어</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr>
<td>pwd</td>
<td>현재 폴더의 위치를 확인한다.</td>
</tr>
<tr>
<td>Is -a</td>
<td>형재 폴더의 파일 목록을 확인한다. <br> -a 옵션을 이용해 숨김 파일도 볼 수 있다.</td>
</tr>
<tr>
<td>cd</td>
<td>홈 폴더로 이동한다. <br> 홈 폴더는 사용자 이름과 폴더명이 길고 내 문서 폴더의 상위 폴더이다.</td>
</tr>
<tr>
<td>cd &lt;폴더이름&gt;</td>
<td>특정 위치의 디렉토리로 이동한다.</td>
</tr>
<tr>
<td>cd …/</td>
<td>현재 폴더의 상위 폴더로 이동한다.</td>
</tr>
<tr>
<td>mkdir &lt;새폴더이름&gt;</td>
<td>현재 폴더의 아래에 새로운 폴더를 만든다.</td>
</tr>
<tr>
<td>echo “Hello Git”</td>
<td>메아리라는 뜻. <br> 화면에 " " 안의 문장인 "Hello Git"을 표시한다.</td>
</tr>
</tbody>
</table><h4 id="git-로컬저장소-생성하기">2) Git 로컬저장소 생성하기</h4>
<ul>
<li>
<p>내 문서로 이동하기</p>
<ul>
<li><code>$ cd Documents/</code>
<ul>
<li>Documents폴더로 이동</li>
</ul>
</li>
<li><code>$ pwd</code>
<ul>
<li>현재 폴더의 위치 확인</li>
</ul>
</li>
</ul>
</li>
<li>
<p>Git 로컬저장소를 위한 새 폴더 만들기</p>
<ul>
<li><code>eunjaeui-MacBookPro:Documents eunjae$ mkdir hello-git-cli</code>
<ul>
<li><code>hello-git-cli</code>라는 이름의 새로운 폴더 생성</li>
</ul>
</li>
<li><code>eunjaeui-MacBookPro:Documents eunjae$ cd hello-git-cli</code>
<ul>
<li>새로 생성한 폴더로 이동</li>
</ul>
</li>
<li><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ pwd</code>
<ul>
<li>현재 폴더 위치 확인</li>
<li><code>/Users/eunjae/Documents/hello-git-cli</code></li>
</ul>
</li>
</ul>
</li>
<li>
<p>Git 로컬 저장소를 위해 만든 새 폴더 정보 보기</p>
<ul>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git status</code></p>
<ul>
<li>git status 명령은 Git 저장소(정확하게는 워킹트리)에서만 정상적으로 수행되는 명령이다.</li>
</ul>

<table>
<thead>
<tr>
<th>명령어</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr>
<td>git statue</td>
<td>git status -s   Git 워킹트리의 상태를 보는 명령으로, 매우 자주 사용한다. <br> 워킹트리가 아닌 폴더에서 실행하면 오류가 발생한다.</td>
</tr>
<tr>
<td>git status -s</td>
<td>git status 명령 보다 짧게 요약해서 상태를 보여주는 명령으로, 변경된 파일이 많을 때 유용하다.</td>
</tr>
</tbody>
</table></li>
<li>
<p>Git 저장소가 아닌 위치에서 <code>$ git status</code> 명령을 수행했는데 오류가 뜨지 않는 경우.</p>
<ul>
<li>새로 만든 폴더가 git 프로젝트의 하위 폴더라는 의미.
<ul>
<li>즉, 해당 폴더의 상위 폴더 중 어떤 폴더가 Git 저장소로 이미 초기화되어 있다는 의미.</li>
<li>Git을 처음 접하는 입문자가 많이하는 실수로 대부분 내 문서(Documents) 폴더가 Git 저장소인 경우가 많다.</li>
<li>이럴 경우 실수로 <code>git push</code>명령을 사용한다면 내 문서 내의 자료가 통채로 GitHub에 공개될 수 있다.</li>
</ul>
</li>
<li>해결방법
<ul>
<li>어딘가에 생성된 <code>[.git]</code>폴더를 삭제해줘야 한다.
<ul>
<li><code>[.git]</code>폴더는 숨김 처리 되어있다.</li>
<li>숨김처리 된 폴더를 보는 방법
<ul>
<li>(mac) command + shift + <code>.</code></li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
<li>
<p>Git 저장소 초기화</p>
<ul>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git init</code></p>
<ul>
<li>Git 저장소 생성</li>
<li><code>Initialized empty Git repository in /Users/eunjae/Documents/hello-git-cli/.git</code></li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ ls -a</code></p>
<ul>
<li>현재 폴더 내 ‘파일 목록’ 확인</li>
<li><code>. .. .git</code> (  ./ …/ .git/ )</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git status</code></p>
<ul>
<li>
<p>워킹 트리 상태 확인</p>
<pre><code>  On branch master     
  
  No commits yet     
     
  nothing to commit (create/copy files and use "git add" to track)
</code></pre>

<table>
<thead>
<tr>
<th>git init</th>
</tr>
</thead>
<tbody>
<tr>
<td>현재 폴더에 Git 저장소를 생성한다. <br> 현재 폴더에는 [.git]이라는 숨김 폴더가 생성되는데 사실 이 폴더가 로컬저장소이다.</td>
</tr>
</tbody>
</table></li>
</ul>
</li>
</ul>
</li>
<li>
<p>워킹트리</p>
<ul>
<li>로컬저장소가 있는 현재 폴더.</li>
<li>즉, 일반적인 작업 폴더를 의미한다.</li>
</ul>
</li>
<li>
<p>Git의 기본적인 용어</p>

<table>
<thead>
<tr>
<th>용어</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr>
<td>워킹트리<br>(working tree)</td>
<td>워크트리, 워킹 디렉토리, 작업 디렉토리, 작업 폴더 모두 같은 뜻으로 사용된다.<br> 일반적으로 사용자가 파일과 하위 폴더를 만들고 작업 결과물을 저장하는 곳을 Git에서는 워킹트리라고 부른다. 공식문서에서는 워킹트리를 '커밋을 체크하웃하면 생성되는 파일과 디렉토리’로 정의하고 있다. 정확하게는 작업 폴더에서 [.git]폴더(로컬저장소)를 뺀 나머지 부분이 워킹드리이다.</td>
</tr>
<tr>
<td>로컬저장소<br>(local repository)</td>
<td>Git init 명령으로 생성되는 [.git]폴더가 로컬저장소이다. 커밋, 커밋을 구성하는 객체, 스테이지가 모두 이 폴더에 저장된다.</td>
</tr>
<tr>
<td>원격저장소<br>(remote reopsitory)</td>
<td>로컬저장소를 업로드하는 곳을 원격저장소라고 한다. 우리가 사용하고 있는 GitHub 저장소가 원격저장소다.(G와 H가 대문자라는 것에 유의)</td>
</tr>
<tr>
<td>Git 저장소</td>
<td>Git 명령으로 관리할 수 있는 폴더 전체를 일반적으로 Git 프로젝트 혹은 Git 저장소라고 부른다. 엄밀하게는 로컬저장소를 의미하지만 넓은 의미로 작업 폴더를 의미하기도 한다.</td>
</tr>
</tbody>
</table></li>
</ul>
<h4 id="옵션-설정하기">3) 옵션 설정하기</h4>
<pre><code>	$ git config --global &lt;옵션명&gt;
		: 지정한 전역 옵션의 내용을 살펴본다.

	$ git config --global &lt;옵션명&gt; &lt;새로운값&gt;
		: 지정한 전역 옵션의 값을 새로 설정

	$ git config --global --unset &lt;옵션명&gt;
		: 지정한 전역 옵션을 삭제

	$ git config --local &lt;옵션명&gt;
		: 지정한 지역 옵션의 내용을 살펴본다.

	$ git config --local &lt;옵션명&gt; &lt;새로운값&gt;
		: 지정한 지역 옵션의 값을 새로 설정

	$ git config --local --unset &lt;옵션명&gt;
		: 지정한 지역 옵션의 값을 삭제

	$ git config --system &lt;옵션명&gt;
		: 지정한 시스템 옵션의 내용을 살펴본다.

	$ git config --system &lt;옵션명&gt; &lt;값&gt;
		: 지정한 시스템 옵션의 값을 새로 설정

	$ git config --system --unset &lt;옵션명&gt; &lt;값&gt;
		: 지정한 시스템 옵션의 값을 삭제

	$ git config --list
		: 현재 프로젝트의 모든 옵션을 살펴본다.
</code></pre>
<ul>
<li>
<p>git config 명령으로 옵션을 보거나, 값을 바꿀 수 있다.</p>
</li>
<li>
<p>Git의 옵션에는 <code>지역 옵션</code>과 <code>전역 옵션</code>, <code>시스템 환경 옵션</code> 에 종류가 있다.</p>
<ul>
<li>시스템 환경 옵션은 Git 저장소에서만 유효한 옵션.</li>
<li>일반적으로 개인 PC에서는 전역 옵션을 사용.</li>
<li>공용 PC나 Git을 써야할 일이 있다면 지역 옵션을 사용.</li>
<li>우선순위는 <code>지역옵션 &gt; 전역옵션 &gt; 시스템옵션</code> 순.<br>
<br></li>
</ul>
</li>
<li>
<p>Git 전역 옵션 설정</p>
<ul>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git config --global user.name</code></p>
<ul>
<li><code>EunJaePark</code> 이라는 결과가 나타났다.
<ul>
<li>현재 설정 된 값이 <code>EunJaePark</code>으로 있다는 의미.</li>
<li>만약, 아무런 결과도 출력되지 않는다면 현재 설정된 값이 없다는 의미로, 바로 새로운 값을 설정하면 된다.</li>
<li>ex) <code>$ git config --global user.name "새로운 이름"</code></li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
<li>
<p>CLI를 사용하면 텍스트 에디터를 쓸 일이 생긴다. 현재 Git Bash의 기본 에디터는 보통 리눅스 운영체제에서 주로 쓰는 vim이나 nano로 설정되어 있다. vim이 뭔지 모를 경우, 기본 에디터를 Visual Studio Code로 변경하는 것이 좋다.</p>
</li>
<li>
<p>Git 기본 에디터 확인</p>
<ul>
<li><code>$ git config core.editor</code></li>
<li><code>$ git config --global core.editor</code></li>
<li><code>$ git config --system core.editor</code></li>
</ul>
</li>
<li>
<p>Git의 기본 에디터를 VSCode로 설정해주자.</p>
<ul>
<li><a href="https://medium.com/@hohpark/vs-code%EB%A5%BC-git-diff-tool%EB%A1%9C-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0-88baa1d9f2b3">해당 블로그 참고</a></li>
</ul>
</li>
</ul>
<br>
<h3 id="기본-cli-명령어-살펴보기">03. 기본 CLI 명령어 살펴보기</h3>
<h4 id="스테이징과-커밋을-수행하는-add-commit">1) 스테이징과 커밋을 수행하는 add, commit</h4>
<ul>
<li>기본적인 git 명령들<pre><code> $ git add 파일1 파일2 ...
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
</code></pre>
</li>
</ul>
<br>
<ul>
<li>
<p>간단한 텍스트 파일을 생성하고 확인하기</p>
<ul>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ echo "hello git"</code></p>
<ul>
<li>화면에 " " 안의 텍스트를 보여준다.</li>
<li><code>hello git</code></li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ echo "hello git" &gt; file1.txt</code></p>
<ul>
<li>" " 안의 텍스트로 file1.txt 파일 생성</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ ls</code></p>
<ul>
<li>현재 폴더의 파일 목록 확인.</li>
<li><code>file1.txt</code> : 방금 생성한 파일이 존재함을 나타내 준다.</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git status</code></p>
<ul>
<li>상태를 살펴봄.<pre><code>On branch master

No commits yet

Untracked files:

(use "git add &lt;file&gt;..." to include in what will be committed)

		file1.txt

nothing added to commit but untracked files present (use "git add" to track)
</code></pre>
</li>
<li>file1.txt라는 파일이 생성되었고, untracked상태임을 확인할 수 있다.</li>
</ul>
</li>
</ul>
</li>
<li>
<p>생성한 파일(변경 내용)을 스테이지에 추가하기</p>
<ul>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git add file1.txt</code></p>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git status</code></p>
<ul>
<li>상태를 확인하면 아래와 같은 결과가 나타남.<pre><code>On branch master

No commits yet

Changes to be committed:
(use "git rm --cached &lt;file&gt;..." to unstage)

new file: file1.txt
</code></pre>
<ul>
<li>새로 만든 file1.txt 파일이 스테이지 영역에 추가된 것을 확인할 수 있다.</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
</ul>
<h4 id="reset-명령으로-스테이징-취소하기">2) reset 명령으로 스테이징 취소하기</h4>
<ul>
<li>
<p>위에 보이는 <code>"git rm --cached &lt;file&gt;..."</code> 명령으로 스테이지에서 내릴 수 있지만, 더 자주 사용하는 명령이 있다.</p>
</li>
<li>
<p><code>$ git reset [파일명]</code></p>
<ul>
<li>스테이지 영역에 있는 파일들을 스테이지에서 내린다(언스테이징).</li>
<li>워킹트리의 내용은 변경되지 않는다. 옵션을 생략할 경우 스테이지의 모든 변경사항을 초기화한다.</li>
<li>reset의 3가지 옵션
<ul>
<li>soft, mixed, hard</li>
<li>옵션 없이 사용하면 기본적으로 mixed reset으로 동작한다.</li>
</ul>
</li>
</ul>
</li>
<li>
<p>스테이지에서 파일 언스테이징하기</p>
<ul>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git reset file1.txt</code></p>
<ul>
<li>file1.txt 파일 언스테이징 (위에서 스테이지에 올려줬던 파일 다시 내림).</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git status</code></p>
<ul>
<li>상태 확인.<pre><code>On branch master

No commits yet

Untracked files:
	(use "git add &lt;file&gt;..." to include in what will be committed)

		file1.txt
		
nothing added to commit but untracked files present (use "git add" to track)
</code></pre>
<ul>
<li>file1.txt 파일이 언스테이징되어 스테이지에서 내려간 상태임을 확인할 수 있다.</li>
</ul>
</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ ls</code></p>
<ul>
<li>현재 폴더의 파일 목록을 확인</li>
<li><code>file1.txt</code></li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ cat file1.txt</code></p>
<ul>
<li>cat 명령으로 파일 내용이 변경되었는지 확인</li>
<li><code>hello git</code></li>
</ul>
</li>
</ul>
</li>
</ul>
<h4 id="cli로-첫-번째-커밋-생성">3) CLI로 첫 번째 커밋 생성</h4>
<ul>
<li>
<p>앞에서 언스테이징을 했으므로 다시 git add 명령을 실행 후 커밋한다. 커밋은 git commit 명령으로 수행한다.</p>
</li>
<li>
<p>첫 번째 CLI 커밋</p>
<ul>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git add file1.txt</code></p>
<ul>
<li>add를 이용해 스테이지에 추가</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git status</code></p>
<ul>
<li>상태 확인</li>
<li>file1.txt가 스테이징 된 것을 확인.<pre><code>On branch master

No commits yet

Changes to be committed:
	(use "git rm --cached &lt;file&gt;..." to unstage)

		new file: file1.txt
</code></pre>
</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git commit</code></p>
<ul>
<li>commit 명령어를 입력하면 VSCode가 열린다.
<ul>
<li>앞서 기본 에디터를 VSCode로 설정해 뒀기 때문.</li>
</ul>
</li>
<li>VScode에서 커밋 메시지를 작성 후 저장하고 VSCode를 닫는다.
<ul>
<li>VSCode에서 커밋 메시지를 작성할 때, 첫 줄과 둘째 줄 사이는 반드시 한 줄 비워줘야한다.</li>
<li>첫 줄에는 작업 내용 요약(제목), 둘째 줄에는 자세하게 작업 내용을 기록(본문).</li>
</ul>
</li>
<li>아래처럼 터미널에 커밋메시지와 커밋되었다는 문구가 나타난다.<pre><code>[master (root-commit) 67352a2] 첫 번째 커밋

1 file changed, 1 insertion(+)

create mode 100644 file1.txt
</code></pre>
</li>
<li>만약 git commit 명령 실행 후, 커밋을 하고싶지 않다면 VSCode에서 아무것도 추가하지 않고 종료해주면 된다.</li>
</ul>
</li>
</ul>
</li>
</ul>
<h4 id="cli로-log-살펴보기">4) CLI로 log 살펴보기</h4>
<ul>
<li>
<p>git log 명령으로 git의 커밋 히스토리 확인해 보기</p>
<ul>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git status</code></p>
<ul>
<li>상태 확인<pre><code>On branch master
nothing to commit, working tree clean
</code></pre>
</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git log --oneline --graph --all --decorate</code></p>
<ul>
<li>
<p>커밋 히스토리 확인</p>
</li>
<li>
<p>'첫 번째 커밋’이라는 메시지로 커밋했던 히스토리가 보인다.</p>
<p><code>* 67352a2 (**HEAD -&gt;** **master**) 첫 번째 커밋</code></p>
<ul>
<li>커밋 히스토리에 보이는 앞의 16진수 7자리 숫자는 커밋 체크섬 혹은 커밋 아이디이다.</li>
<li>실제로 커밋 체크섬은 40자리인데 앞의 7자리만 화면에 보여진다.</li>
<li>SHA1해시 체크섬 값을 사용하는 것으로, 전 세계에서 유일한 값을 가진다. (모든 커밋의 아이디가 다르다는 말)</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
<li>
<p>git log의 다양한 옵션</p>
<pre><code> $ git log
	 : 현재 브랜치의 커밋 이력을 보는 명령

 $ git log -n&lt;숫자&gt;
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
</code></pre>
<ul>
<li>각각의 옵션의 조합에 따라 결과가 달라진다.<pre><code> $ git log
	: HEAD와 관련된 커밋들이 자세하게 나온다.

 $ git log --oneline
	 : 간단히 커밋 해시와 제목만 보고 싶을 때

 $ git log --oneline --graph --decorate
	 : HEAD와 관련된 커밋들을 조금 터 자세히 보고 싶을 때

 $ git log --oneline --graph --all --decorate
	 : 모든 브랜치들을 보고 싶을 때

 $ git log --oneline -n5	
	 : 내 브랜치의 최신 커밋을 5개만 보고 싶을 때
</code></pre>
</li>
</ul>
</li>
<li>
<p>좋은 커밋 메시지의 7가지 규칙</p>
<ol>
<li>제목과 본문을 빈 줄로 분리한다.</li>
<li>제목은 50자 이내로 쓴다.</li>
<li>제목을 영어로 쓸 경우 첫 글자는 대문자로 쓴다.</li>
<li>제목에는 마침표를 넣지 않는다.</li>
<li>제목을 영어로 쓸 경우 동사원형(현재형)으로 시작한다.</li>
<li>본문을 72자 단위로 줄바꿈한다.</li>
<li>어떻게 보다 무엇과 왜를 설명한다.</li>
</ol>
</li>
</ul>
<h4 id="도움말-기능-사용하기">5) 도움말 기능 사용하기</h4>
<ul>
<li>
<p>Git에는 각 명령의 도움말을 볼 수 있는 명령이 있다.</p>
</li>
<li>
<p><code>$ git help &lt;명령어&gt;</code></p>
<ul>
<li>해당 명령어의 도움말을 표시</li>
<li>도움말에는 명려으이 의미와 세부적인 옵션들이 매우 자세하게 표시된다.</li>
</ul>
</li>
<li>
<p>git 도움말 사용해 보기</p>
<ul>
<li><code>$ git help status</code></li>
<li><code>$ git help commit</code></li>
<li><code>$ git help add</code></li>
</ul>
</li>
<li>
<p>$ git help ~ 를 사용 후 빠져나오려면 <code>q</code>자판을 눌러주면 된다.</p>
</li>
</ul>
<br>
<h3 id="원격저장소-관련-cli-명령어">04. 원격저장소 관련 CLI 명령어</h3>
<h4 id="remote-push-pull">1) remote, push, pull</h4>
<ul>
<li>
<p>커밋을 했으니 원격저장소에 push를 보내야 한다.</p>
</li>
<li>
<p><code>$ git remote add &lt;원격저장소 이름&gt; &lt;원격저장소 주소&gt;</code></p>
<ul>
<li>원격저장소 등록.</li>
<li>원격저장소는 여러 개 등록할 수 있지만 같은 별명의 원격저장소는 하나만 가질 수 있다. 통상 첫 번째 원격저장소를 origin으로 지정한다.</li>
</ul>
</li>
<li>
<p><code>$ git remote -v</code></p>
<ul>
<li>원격저장소 목록을 살펴본다.</li>
</ul>
</li>
<li>
<p>원격저장소 등록 및 push</p>
<ul>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git remote add origin https://github.com/EunJaePark/hello-git-cli.git</code></p>
<ul>
<li>새로 생성한 원격저장소 등록.</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git remote -v</code></p>
<ul>
<li>원격저장소 목록을 살펴 봄<pre><code>origin  https://github.com/EunJaePark/hello-git-cli.git (fetch)
origin  https://github.com/EunJaePark/hello-git-cli.git (push)
</code></pre>
</li>
</ul>
</li>
<li>
<p>push해줌<br>
`eunjaeui-MacBookPro:hello-git-cli eunjae$ git push```</p>
<ul>
<li>실패했다는 에러 메시지 나옴.<pre><code>fatal: The current branch master has no upstream branch.
To push the current branch and set the remote as upstream, use

	git push --set-upstream origin master
</code></pre>
<ul>
<li>로컬저장소의 [master] 브랜치와 연결된 원격저장소의 브랜치가 없어서 발생한 오류이다.</li>
<li>upstream 브랜치는 로컬저장소와 연결된 원격저장소를 일컫는 단어이다.</li>
<li>에러메시지에서 알려준 대로 <code>--set-upstream</code>을 쓰거나 이 명령의 단축 명령인 <code>-u</code> 옵션을 사용한다.</li>
<li>이후에는 origin 저장소의 [master]브랜치가 로컬저장소의 [master] 브랜치의 업스트림으로 지정되어 <code>git push</code>명령어만으로도 에러 없이 push가 가능해진다.</li>
<li>참고로 Git Bash에서 긴 명령은 <code>--</code>(대시 두 개)로, 짧은 명령은 <code>-</code>(대시 한 개)로 시작하는 경우가 많다.</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
<li>
<p>git push 재시도</p>
<ul>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git push -u origin master</code></p>
<ul>
<li>push와 동시에 업스트림 지정<pre><code>Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 302 bytes | 302.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/EunJaePark/hello-git-cli.git
* [new branch]  master -&gt; master
Branch 'master' set up to track remote branch 'master' from 'origin'.
</code></pre>
</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git log --oneline -n1</code></p>
<ul>
<li>브랜치의 최신 커밋 1개만 확인<pre><code>b6e1657 (**HEAD -&gt;** **master**, **origin/master**) 첫 번째 커밋
</code></pre>
</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git push</code></p>
<ul>
<li>다시 push 해 줌</li>
<li><code>Everything up-to-date</code></li>
</ul>
</li>
<li>
<p>이전 GUI실습 때 내 컴퓨터의 keychain을 새로 생성한 두 번째 GitHub계정으로 바꿔놔서 push재시도에서 헤맸다.</p>
<ul>
<li>다시 keychain을 기존 깃헙 계정으로 수정해주니까 push 재시도 성공했다.</li>
<li>폴더, 파일, 원격저장소 생성 다시 처음부터 해보았는데도 실패해서 좌절했었음…ㅠ…</li>
</ul>
</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git log</code></p>
<ul>
<li>git log 명령을 통해 확인.<pre><code>commit b6e1657dcdcee7babe501dfecf9e4d84058d27e7 (**HEAD -&gt;** **master**, **origin/master**)

Author: EunJaePark &lt;design0728@naver.com&gt;

Date: Mon Jun 22 14:34:31 2020 +0900

  

첫 번째 커밋

간단하게 hello git이라고 쓴 내용을 커밋했다.
</code></pre>
<ul>
<li>HEAD는 [master]를 가르키고 있고, [origin/master]브랜치도 생겨난 것을 볼 수 있다.</li>
<li>HEAD가 가리키는 [master]는 로컬의 [master]브랜치이고, [origin/master]는 원격저장소인 GitHub의 마스터 브랜치이다.</li>
</ul>
</li>
</ul>
</li>
</ul>
<h4 id="clone">2) clone</h4>
<ul>
<li>
<p>CLI로 clone을 해보자.</p>
</li>
<li>
<p><code>$ git clone</code> 명령을 사용할 때, 저장소 주소가 꼭 원격일 필요는 없다. 때에 따라 로컬저장소를 클론으로 복제하면 편리하게 사용할 수 있다.</p>
</li>
<li>
<p>git clone 사용해 보기</p>
<ul>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ pwd</code></p>
<ul>
<li>현재 위치 확인			<br>
<code>/Users/eunjae/Documents/hello-git-cli</code></li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ cd ../</code></p>
<ul>
<li>상위 디렉토리로 이동!</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:Documents eunjae$ git clone https://github.com/EunJaePark/hello-git-cli.git</code></p>
<ul>
<li>원격저장소를 clone으로 복제 시도<pre><code>fatal: destination path 'hello-git-cli' already exists and is not an empty directory.
</code></pre>
<ul>
<li>실패.</li>
<li>[새로운 폴더명] 옵션을 지정하지 않으면 복제한 프로젝트 이름과 같은 폴더를 만들게 되는데, 이미 [hello-git-cli]라는 폴더가 있기 때문에 실패한 것.</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
<li>
<p>git clone으로 로컬저장소 복제하기([새로운 폴더명] 옵션 사용)</p>
<ul>
<li>
<p><code>eunjaeui-MacBookPro:Documents eunjae$ git clone https://github.com/EunJaePark/hello-git-cli.git hello-git-cli2</code></p>
<ul>
<li>새로운 폴더명  <code>hello-git-cli2</code>를 설정해 클론<pre><code>Cloning into 'hello-git-cli2'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
</code></pre>
</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:Documents eunjae$ ls</code></p>
<ul>
<li>Documents에 들어있는 폴더 확인<pre><code>hello-git-cli
hello-git-cli2
movie
터미널에서 저장된 출력
</code></pre>
</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:Documents eunjae$ cd hello-git-cli2</code></p>
<ul>
<li>클론한 폴더로 위치 이동</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli2 eunjae$ git log --oneline</code></p>
<ul>
<li>간단한 커밋 정보 확인<pre><code>b6e1657 (**HEAD -&gt;** **master**, **origin/master**, **origin/HEAD**) 첫 번째 커밋
</code></pre>
</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli2 eunjae$ git remote -v</code></p>
<ul>
<li>원격저장소 목록 확인<pre><code>origin  https://github.com/EunJaePark/hello-git-cli.git (fetch)

origin  https://github.com/EunJaePark/hello-git-cli.git (push)
</code></pre>
</li>
</ul>
</li>
</ul>
</li>
<li>
<p>추가 commit and push(클론한 저장소에서 커밋해보기)</p>
<ul>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli2 eunjae$ echo "second" &gt;&gt; file1.txt</code></p>
<ul>
<li>file1.txt 파일에 'second’라는 내용 추가</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli2 eunjae$ cat file1.txt</code></p>
<ul>
<li>file1.txt파일의 내용 확인<pre><code>hello git

second
</code></pre>
</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli2 eunjae$ git commit -a</code></p>
<ul>
<li>스테이징 없이 바로 커밋<pre><code>[master 2ec7e32] 두 번째 커밋

1 file changed, 1 insertion(+)
</code></pre>
</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli2 eunjae$ git push</code></p>
<ul>
<li>수정한 파일 push<pre><code>Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Writing objects: 100% (3/3), 286 bytes | 286.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/EunJaePark/hello-git-cli.git
	b6e1657..2ec7e32  master -&gt; master
</code></pre>
</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli2 eunjae$ git log --oneline</code></p>
<ul>
<li>커밋 정보 간단하게 확인<pre><code>2ec7e32 (**HEAD -&gt;** **master**, **origin/master**, **origin/HEAD**) 두 번째 커밋

b6e1657 첫 번째 커밋
</code></pre>
</li>
</ul>
</li>
</ul>
</li>
</ul>
<br>
<ul>
<li>다시 첫 번째 저장소로 돌아가서 두 번째 저장소에서 변경한 내용을 내려받아보자. ( <code>git pull</code>)
<ul>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli2 eunjae$ cd ~/Documents/hello-git-cli</code></p>
<ul>
<li>처음 저장소로 이동</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git log --oneline</code></p>
<ul>
<li>결과를 보면 기존에 커밋한 첫 번째 커밋만 있음을 알 수 있다.<pre><code>b6e1657 (**HEAD -&gt;** **master**, **origin/master**) 첫 번째 커밋
</code></pre>
</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git pull</code></p>
<ul>
<li>두 번째 저장소의 변경사항을 내려받음<pre><code>remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/EunJaePark/hello-git-cli
	b6e1657..2ec7e32  master -&gt; origin/master
Updating b6e1657..2ec7e32
Fast-forward
	file1.txt | 1 +
	1 file changed, 1 insertion(+)
</code></pre>
</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ git log --oneline</code></p>
<ul>
<li>커밋을 다시 확인해보면 두 번째 저장소에서 커밋한 내용이 추가되었음을 보여준다.<pre><code>2ec7e32 (**HEAD -&gt;** **master**, **origin/master**) 두 번째 커밋
b6e1657 첫 번째 커밋
</code></pre>
</li>
</ul>
</li>
<li>
<p><code>eunjaeui-MacBookPro:hello-git-cli eunjae$ cat file1.txt</code></p>
<ul>
<li>file1.txt의 내용을 확인해 보면 수정된 내용이 추가된 것을 볼 수 있다.<pre><code>hello git
second
</code></pre>
</li>
</ul>
</li>
</ul>
</li>
</ul>
<br>
<ul>
<li>처음 생성했던 Git 저장소로 이동한 후 git pull 명령을 수행했다. <code>pull</code>이란 <code>fetch</code>와 <code>merge</code>를 합친 것이라고 보면 된다.</li>
</ul>

