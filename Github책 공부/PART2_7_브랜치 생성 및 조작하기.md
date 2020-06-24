
### 01. CLI로 브랜치 생성하기
#### 1) branch 되돌아 보기
- HEAD : 현재 작업중인 브랜치
- 1) 커밋하면 커밋 객체가 생긴다. 커밋 객체에는 부모 커밋에 대한 참조와 실제 커밋을 구성하는 파일 객체가 들어 있다.       
	2) 브랜치는 논리적으로는 어떤 커밋과 그 조상들을 묶어서 뜻하지만, 사실은 단순히 커밋 객체 하나를 가리킨다. 
	
- 브랜치를 언제 사용하나?
	- 새로운 기능 추가
	- 버그 수정
	- 병합과 리베이스 테스트
	- 이전 코드 개선
	- 특정 커밋으로 돌아가고 싶을 때

#### 2) 브랜치 생성하기
```
 $ git branch [-v]
	 : 로컬 저장소 브랜치 목록을 보는 명령.  
	   -v 옵션을 사용하면 마지막 커밋도 함께 표시된다.     
	   표시된 브랜치 중에서 이름 왼쪽에 *가 붙어 있으면 HEAD브랜치이다.
	   
 $ git branch [-f] <브랜치이름> [커밋체크섬]
	 : 새로운 브랜치를 생성.     
	   커밋체크섬 값을 주지 않으면 HEAD로부터 브랜치를 생성한다.   
	   이미 있는 브랜치를 다른 커밋으로 옮기고 싶을 때는 -f 옵션을 줘야 한다.
	   
 $ git branch -r[v]
	 : 원격 저장소에 있는 브랜치를 보고 싶을 때 사용.   
	   -v 옵션을 추가하여 커밋 요약도 볼 수 있다.
	   
 $ git checkout <브랜치이름>
	 : 특정 브랜치로 체크아웃할 때 사용.   
	   브랜치 이름 대신 커밋 체크섬을 쓸 수 있다.(하지만 브랜치 이름을 쓰는 방법을 강력히 권장)
	   
 $ git check -b <브랜치이름> <커밋 체크섬>
	 : 특정 커밋에서 브랜치를 새로 생성하고 동시에 체크아웃까지 함.   
	   두 명령을 하나로 합친 명령이기 때문에 간결해서 자주 사용.
	   
 $ git merge <대상 브랜치>
	 : 현재 브랜치와 대상 브랜치를 병합할 때 사용.   
	   병합 커밋(merge commit)이 새로 생기는 겨우가 많다.
	   
 $ git rebase <대상 브랜치>
	 : 내 브랜치의 커밋들을 대상 브랜치에 재배치.   
	   히스토리가 깔끔해져서 자주 사용하지만 조심해야한다.
	   
 $ git brancch -d <브랜치이름>
	 : 특정 브랜치를 삭제.    
	   HEAD 브랜치나 병합되지 않은 브랜치는 삭제 불가.
	   
 $ git branch -D <브랜치이름>
	 : 브랜치를 강제로 삭제.
	   -d로 삭제할 수 없는 브랜치를 지우고 싶을 때 사용.
	   조심해서 사용해야 함.
```

- 브랜치 만들기
	- `(master) $ git log --oneline`
		- 커밋 로그 보기
		- 현재 커밓과 브랜치 상태 확인
			```
				2ec7e32 (HEAD -> master, origin/master) 두 번째 커밋
				b6e1657 첫 번째 커밋
			```
		
	- `(master) $ git branch`
		- 현재 브랜치 확인
		- `* master`는 `HEAD -> master`와 동일한 의미이다.
		   ```
		    * master
		  ```
		  
	- `(master) $ git branch mybranch1`
		- `mybranch1`이라는 이름의 새로운 브랜치 생성
		
	- `(master) $ git branch`
		- 현재 브랜치 확인
			```
			* master
			  mybranch1
			```
			
	- `(master) $ git log --oneline --all`
		- 변경된 브랜치 확인
		- 아직 체크아웃 전이기 때문에 여전히 HEAD는 [master] 브랜치를 가리키고 있는 상태.
		   ```
		    2ec7e32 (HEAD -> master, origin/master, mybranch1) 두 번째 커밋
		    b6e1657 첫 번째 커밋
			```

- HEAD에 대해 반드시 기억할 것
	1. HEAD는 현재 작업 중인 브랜치를 가리킨다.
	2. 브랜치는 커밋을 가리키므로 HEAD도 커밋을 가리킨다.
	3. 결국 HEAD는 현재 작업 중인 브랜치의 최근 커밋을 가리킨다.

<br/>

### 02. CLI로 checkout 하기
- checkout 명령은 브랜치의 내용을 워킹트리에 반영할 때 사용한다. (브랜치가 가리키고 있는 커밋의 내용을 반영하는 것)

#### 1) CLI를 이용한 브랜치 체크아웃 및 새 커밋 생성
- 브랜치 만들기
	```
	 (master)$ git checkout mybranch1   # 브랜치 체크아웃	
		 ---->  Switched to branch 'master'
	 
	 (mybranch1)$ git branch   # 현재브랜치 확인
		 ----> master
	           	* mybranch1
	           	===> mybranch1으로 체크아웃해줘서 *표시가 mybranch1앞으로 옮겨진 상태
	           
	 (mybranch1)$ git log --oneline --all   # HEAD 변경 확인
		 ----> 2ec7e32 (HEAD -> mybranch1, origin/master, master) 두 번째 커밋
	           	b6e1657 첫 번째 커밋

	 (mybranch1)$ cat file1.txt   # 파일 내용 확인
		 ----> hello git
	           	second
	 (mybranch1)$ echo "third - my branch" >> file1.txt   # 파일에 내용 추가

	 (mybranch1)$ car file1.txt   # 변경 내용 확인
		 ----> hello git
	           	second
	           	third - my branch

	 (mybranch1)$ git status   # 스테이지 상태 확인
		 ----> On branch mybranch1
			Changes not staged for commit:
			   (use "git add <file>..." to update what will be committed)
			   (use "git checkout -- <file>..." to discard changes in working directory)

					modified: file1.txt

			 no changes added to commit (use "git add" and/or "git commit -a")

	 (mybranch1)$ git add file1.txt   # 스테이지에 변경사항 추가

	 (mybranch1)$ git commit   # 커밋
		 ----> [mybranch1 0c8e721] mybranch1의 첫 번째 커밋
	                1 file changed, 1 insertion(+)

	 (mybranch1)$ git log --oneline --all   # 변경된 브랜치 확인
		 ----> 0c8e721 (HEAD -> mybranch1) mybranch1의 첫 번째 커밋
		       2ec7e32 (origin/master, master) 두 번째 커밋
		       b6e1657 첫 번째 커밋
	 
	```

#### 2) CLI를 이용한 빨리 감기 병합
- 앞서 커밋한 [mybranch1] 브랜치에서 추가로 한 번 더 커밋을 하고 [master] 브랜치로 체크아웃 후, [master] 브랜치와 [mybranch1] 브랜치를 병합해보자.

- 커밋 후 빨리 감기 병합
	```
	 (mybranch1)$ echo "four - my branch" >> file1.txt   # 파일에 내용 추가

	 (mybranch1)$ cat file1.txt   # 파일 내용 확인
		 ---> hello git
		      second
		      third - my branch
		      four - my branch

	 (mybranch1)$ git status   # 스테이지 상태 확인
		 ----> On branch mybranch1
			Changes not staged for commit:
			   (use "git add <file>..." to update what will be committed)
			   (use "git checkout -- <file>..." to discard changes in working directory)	  

			        modified: file1.txt

			no changes added to commit (use "git add" and/or "git commit -a")

	 (mybranch1)$ git add file1.txt   # 스테이지에 추가

	 (mybranch1)$ git commit   # 신규 커밋 추가
		 ----> [mybranch1 ea16908] 두 번째 커밋
			1 file changed, 1 insertion(+)

	 (mybranch1)$ git log --oneline --all --graph   # 커밋 로그 보기
		----> * ea16908 (HEAD -> mybranch1) 두 번째 커밋
		      * 0c8e721 mybranch1의 첫 번째 커밋
		      * 2ec7e32 (origin/master, master) 두 번째 커밋
		      * b6e1657 첫 번째 커밋
		      ===> 기존 커밋을 부모로 하는 새로운 커밋이 생성되었음을 알 수 있다.
		      ===> HEAD는 mybranch1, mybranch1은 새 커밋을 각각 가리키는 것을 확인할 수 있다.

	 (mybranch1)$ git checkout master   # 마스터 브랜치 체크아웃
		 ----> Switched to branch 'master'
			Your branch is up to date with 'origin/master'.

	 (master)$ cat file1.txt   # 파일이 이전으로 돌아갔는지 확인
		 ----> hello git
			second

	 (master)$ git merge mybranch1   # 병합, Fast-forward
		 ----> Updating 2ec7e32..ea16908
			Fast-forward
			  file1.txt | 2 ++
			  1 file changed, 2 insertions(+)
			===> [master]브랜치에 [mybranch1]브랜치를 병합했다.
			===> Fast-forward = 빨리 감기 병합

	 (master)$ git log --oneline --all --graph   # 로그 확인
		 ----> * ea16908 (HEAD -> master, mybranch1) 두 번째 커밋
			* 0c8e721 mybranch1의 첫 번째 커밋
			* 2ec7e32 (origin/master) 두 번째 커밋
			* b6e1657 첫 번째 커밋
	 
	 (master)$ cat file1.txt   # 파일 상태 재확인
		 ----> hello git
			second
			third - my branch
			four - my branch
	```

#### 3) reset --hard로 브랜치 되돌리기
- reset은 현재 브랜치를 특정 커밋으로 되돌릴 때 사용한다.
- `git reset --hard  <이동할 커밋 체크섬>`
	- 명령을 실행하면 현재 브랜치를 지정한 커밋으로 옮긴 후, 해당 커밋의 내용을 작업 폴더에도 반영한다.
	- `git reset --hard`명령을 사용하려면 커밋 체크섬을 알아야 한다.
		- 커밋 체크섬은 `git log`를 통해 확인할 수도 있지만, 간단하게 `HEAD~` 또는 `HEAD^`로 시작하는 약칭을 사용할 수 있다.

- `HEAD~`, `HEAD^`
	- `HEAD~<숫자>`
		- `HEAD~`은 헤드의 부모 커밋, `HEAD~2`는 헤드의 할아버지 커밋을 말한다. 
		- `HEAD~n`은 n번째 위쪽 조상이라는 뜻.
		
	- `HEAD^<숫자>`
		- `HEAD^`은 똑같이 부모 커밋이다. 반면 `HEAD^2`는 두 번째 부모를 가르킨다.
		- 병합 커밋처럼 부모가 둘 이상인 커밋에서만 의미가 있다.

- 현재 브랜치를 두 단계 이전으로 되돌리기
	- `$ git reset --hard HEAD~2`
		- 브랜치 되돌리기
		- `HEAD~2`를 입력해 2단계 이전으로 되돌림.
			```
			 HEAD is now at 2ec7e32 두 번째 커밋
			```
	
	- `$ git log --oneline --all`
		- 로그 확인
		- `HEAD -> master`가 달라진 것을 알 수 있다.
			```
			 ea16908 (mybranch1) 두 번째 커밋
			 0c8e721 mybranch1의 첫 번째 커밋
			 2ec7e32 (HEAD -> master, origin/master) 두 번째 커밋
			 b6e1657 첫 번째 커밋
			```

#### 4) 빨리 감기 병합 상황에서 rebase 해보기
```
 $ git checkout mybranch1   # 브랜치 변경
	 ----> Switched to branch 'mybranch1'

 $ git rebase master   # rebase(재배치) 시도
	 ----> Current branch mybranch1 is up to date.

 $ git log --oneline --all   # 로그 확인, 변화 없음
	 ----> ea16908 (HEAD -> mybranch1) 두 번째 커밋
	       0c8e721 mybranch1의 첫 번째 커밋
	       2ec7e32 (origin/master, master) 두 번째 커밋
	       b6e1657 첫 번째 커밋
	       ===> [mybranch1]브랜치는 이미 [master]브랜치 위에 있기 때문에 재배치할 커밋이 없는 것이다.

 $ git checkout master   # 다시 master 브랜치 체크아웃
	 ----> Switched to branch 'master'
	       Your branch is up to date with 'origin/master'.

 $ git rebase mybranch1   # 반대 방향에서 rebase
	 ----> First, rewinding head to replay your work on top of it...
	       Fast-forwarded master to mybranch1.

 $ git log --oneline --all   # 변경 사항을 확인해 보면 빨리 감기 병합이 되었다.
	 ----> ea16908 (HEAD -> master, mybranch1) 두 번째 커밋
	       0c8e721 mybranch1의 첫 번째 커밋
	       2ec7e32 (origin/master) 두 번째 커밋
	       b6e1657 첫 번째 커밋
	       ===> 빨리감기가 가능한 상황이기 때문에 rebase는 merge 명령과 마찬가지로 빨리감기를 하고 작업을 종료한다.

 $ git push   # push
	 ----> Enumerating objects: 8, done.
	       Counting objects: 100% (8/8), done.
	       Delta compression using up to 12 threads
	       Compressing objects: 100% (3/3), done.
	       Writing objects: 100% (6/6), 593 bytes | 593.00 KiB/s, done.
	       Total 6 (delta 0), reused 0 (delta 0)
	       To https://github.com/EunJaePark/hello-git-cli.git
	       2ec7e32..ea16908  master -> master

 $ git branch -d mybranch1   # 브랜치 삭제
	 ----> Deleted branch mybranch1 (was ea16908).
		===> 필요없어진 [mybranch1] 브랜치를 삭제.

 $ git log --oneline --all -n2   # 로그 확인
	 ----> ea16908 (HEAD -> master, origin/master) 두 번째 커밋
	       0c8e721 mybranch1의 첫 번째 커밋
```

#### 5) 배포 버전에 태깅하기
- 태그(tag)는 `주석 있는 태그`, `간단한 태그` 두 종류가 있다.
	- 일반적으로 주석 있는 태그의 사용을 권장.
	
- `$ git tag -a -m <간단한 메시지> <태그 이름> [브랜치 또는 체크섬]`
	- `-a`로 주석 있는(annotated) 태그를 생성한다. 
	- 메시지와 태그 이름은 필수이며 브랜치 이름을 생략하면 HEAD에 태그를 생성한다.
	
- `$ git push <원격저장소 별명> <태그 이름>`
	- 원격 저장소 태그를 업로드한다.

- tag 작성
	- `$ git log --oneline`
		- 로그 확인
			```
			 ea16908 (**HEAD ->** **master**, **origin/master**) 두 번째 커밋
			 0c8e721 mybranch1의 첫 번째 커밋
			 2ec7e32 두 번째 커밋
			 b6e1657 첫 번째 커밋	
			```	

	- `$ git tag -a -m "첫 번째 태그 생성" v0.1`
		- 주석 있는 태그 작성

	- `$ git log --oneline`
		- 태그 생성 확인
		  ```
			ea16908 (**HEAD ->** **master**, **tag: v0.1**, **origin/master**) 두 번째 커밋
			0c8e721 mybranch1의 첫 번째 커밋
			2ec7e32 두 번째 커밋
			b6e1657 첫 번째 커밋	
			```

	- `$ git push origin v0.1`
		- 태그 푸시
			```
			 Enumerating objects: 1, done.
			 Counting objects: 100% (1/1), done.
			 Writing objects: 100% (1/1), 192 bytes | 192.00 KiB/s, done.
			 Total 1 (delta 0), reused 0 (delta 0)
			 To https://github.com/EunJaePark/hello-git-cli.git
			 * [new tag] v0.1 -> v0.1
			```
<br/>

- 태그(tag)는 차후에 커밋을 식별할 수 있는 유용한 정보이다.
- 태그를 사용하면 GitHub의 [Tag] 탭에서 확인할 수 있으며, [Release] 탭에서 다운받을 수도 있다.

<br/>

### 03. CLI로 3-way 병합하기
#### 1) 긴급한 버그 처리 시나리오
- 새로운 브랜치 및 커밋 생성
	-	`$ git checkout master`
		-	master로 체크아웃

	- `$ git checkout -b feature1`
		- feature1 브랜치 생성 및 체크아웃
			```
			 Switched to a new branch 'feature1'
			```

	- `$ echo "기능 1 추가" >> file1.txt`
		- 파일 내용 수정

	- `$ git add file1.txt`
		- 스테이징

	- `$ git commit`
		- 커밋
			```
			 [feature1 c259819] 새로운 기능 1 추가
			 1 file changed, 1 insertion(+)
			```

	- `$ git log --oneline --graph --all -n2`
		- 로그 확인
			```
			 * c259819 (**HEAD ->** **feature1**) 새로운 기능 1 추가
			 * ea16908 (**tag: v0.1**, **origin/master**, **master**) 두 번째 커밋
			 ```

- 지금 이 시점에서 장애가 발생했다고 가정하고, 버그를 고치기 위해 [master]브랜치에서 [hotfix]브랜치를 만든다. 그리고 버그를 고친 후 커밋한다. 그 후, [hotfix]브랜치를 [master]브랜치에 병합한다.
- [master]브랜치의 최신 커밋을 기반으로 [hotfix]브랜치 작업을 했기 때문에 빨리 감기 병합기 가능한 상황이 된다.
<br/>

- hotfix 브랜치 생성, 커밋, master에 병합
	```
	 $ git  checkout -b hotfix master   # master로부터 hotfix 브랜치 생성, 체크아웃
		 ----> Switched to a new branch 'hotfix'

	 $ git log --oneline --all -n2   # 2개의 커밋 로그만 보기
		 ----> c259819 (**feature1**) 새로운 기능 1 추가
		       ea16908 (**HEAD ->** **hotfix**, **tag: v0.1**, **origin/master**, **master**) 두 번째 커밋

	 $ echo "some hot fix" >> file1.txt

	 $ git add file1.txt

	 $ git commit
		 ----> [hotfix 209e069] hotfix 실습
			   1 file changed, 1 insertion(+)

	 $ git log --oneline -n1
		 ----> 	209e069 (**HEAD ->** **hotfix**) hotfix 실습

	 $ git checkout master
	 	----> Switched to branch 'master'
		      Your branch is up to date with 'origin/master'.

	 $ git merge hotfix   # 빨리 감기 병합
		 ----> Updating ea16908..209e069
			Fast-forward
			   file1.txt | 1 +
			   1 file changed, 1 insertion(+)

	 $ git push   # 원격저장소로 push
		 ----> Enumerating objects: 5, done.
			Counting objects: 100% (5/5), done.
			Delta compression using up to 12 threads
			Compressing objects: 100% (2/2), done.
			Writing objects: 100% (3/3), 309 bytes | 309.00 KiB/s, done.
			Total 3 (delta 0), reused 0 (delta 0)
			To https://github.com/EunJaePark/hello-git-cli.git
			    ea16908..209e069  master -> master
	```
	- 위의 버그 수정 사항을 현재 개발 중인 [feature1] 브랜치에도 반영해줘야 한다.
	
	- [feature1] 브랜치와 [master] 브랜치는 다른 분기로 진행중인 상태이다. 이 경우에는 빨리 감기 병합이 불가능하므로 3-way 병합을 해줘야 한다.     
	   ---> 병합 커밋이 생성될 것이다.
	   
	 - 3-way병합이 항상 충돌을 일으키는 것은 아니지만, 이번 실습에서는 고의적으로 두 브랜치 모두 file1.txt를 수정했기 때문에 충돌이 발생할 것이다.
	 
		|     master 브랜치의 file1.txt | feature1 브랜치의 file1.txt |
		| ------------------------------- | ------------------------------ |
		|    hello git <br/> second <br/> third - my branch <br/> fourth <br/> **some hot fix** | hello git <br/> second <br/> third - my branch <br/> fourth <br/> **신규기능1** |
		
<br/>

- 병합 및 충돌 해결하기1
```
 $ git checkout feature1   # feature1 브랜치 체크아웃
	 ----> Switched to branch 'feature1'

 $ git log --oneline --all   # 로그 확인
	 ----> 209e069 (**origin/master**, **master**, **hotfix**) hotfix 실습
		c259819 (**HEAD ->** **feature1**) 새로운 기능 1 추가
		ea16908 (**tag: v0.1**) 두 번째 커밋
		0c8e721 mybranch1의 첫 번째 커밋
		2ec7e32 두 번째 커밋
		b6e1657 첫 번째 커밋

 $ git merge master   # master 브랜치와 병합 시도
	 ----> Auto-merging file1.txt
		CONFLICT (content): Merge conflict in file1.txt
		Automatic merge failed; fix conflicts and then commit the result.
		===> git merge master 명령이 충돌로 인해 실패했다.

 $ git status   # 실패 원인 파악하기
	 ----> On branch feature1
		You have unmerged paths.
		    (fix conflicts and run "git commit")
		    (use "git merge --abort" to abort the merge)

	        Unmerged paths:
		    (use "git add <file>..." to mark resolution)

		         both modified: file1.txt

		no changes added to commit (use "git add" and/or "git commit -a")
		===> 충돌 대상 파일을 확인.
		===> 결과 메시지에서 볼 수 있는 것처럼 git merge --abort 명령을 통해 merge를 취소할 수도 있다.
```
- VSCode에서 충돌이 일어난 파일을 열어 [두 변경 사항 모두 수락]을 눌러 수정해준다.
- 수정 내용을 저장하고 다시 스테이지에 추가 및 커밋을 하면 수동 3-way 병합이 완료된다.
<br/>

- 병합 및 충돌 해결하기2
```
 $ cat file1.txt   # 최종 변경 내용 확인
	 ----> hello git
		second
		third - my branch
		four - my branch
		기능 1 추가
		some hot fix

 $ git add file1.txt   # 스테이징

 $ git status
	 ----> On branch feature1
	       All conflicts fixed but you are still merging.
		  (use "git commit" to conclude merge)

	       Changes to be committed:

		          modified: file1.txt
	       ===> git add 및 git status를 수행하면 충돌한 파일의 수정을 완료한 후에 git commit 명령을 수행하면 된다는 것을 알 수 있다.
  
 $ git commit   # 머지 커밋 생성
	 ----> [feature1 231f9c7] Merge branch 'master' into feature1

 $ git log --oneline --all --graph -n4   # 로그 확인
	 ----> * 231f9c7 (**HEAD ->** **feature1**) Merge branch 'master' into feature1
	       |\
	       | * 209e069 (**origin/master**, **master**, **hotfix**) hotfix 실습
	       * |  c259819 새로운 기능 1 추가
	       |/
	       * ea16908 (**tag: v0.1**) 두 번째 커밋
	       ===> git commit 명령으로 충돌난 3way 병합을 마무리 짓는다. 
	       ===> 병합 커밋이므로 커밋 메시지는 굳이 편집하지 않고 저장 후 에디터를 빠져 나오면 된다.
```

<br/>

### 04. CLI로 rebase 해 보기
#### 1) rebase 사용하기
- rebase의 원리
	1. HEAD와 대상 브랜치의 공통 조상을 찾는다.
	2. 공통 조상 이후에 생성한 커밋들을 대상 브랜치 뒤로 재배치한다.

- rebase 명령어는 주로 로컬 브랜치를 깔끔하게 정리하고 싶을 때 사용.
- rebase 명령을 실행하면 대상 브랜치 뒤로 재배치된 커밋들은 rebase전의 커밋과 다르다고 보면 된다.(내용물은 같지만 다른 존재라고 생각하면 됨)

- 원격저장소에 존재하는 브랜치에 대해서는 rebase를 하지 않는 것이 좋다.

- reset --hard 및 rebase 시도
	```
	eunjaeui-MacBookPro:hello-git-cli eunjae$ git checkout feature1   # HEAD를 feature1으로 전환. 이미 HEAD일 경우 생략 가능
		---> Already on 'feature1'

	eunjaeui-MacBookPro:hello-git-cli eunjae$ git reset --hard HEAD~   # 현재 브랜치를 한 단계 되돌린다
		---> HEAD is now at c259819 새로운 기능 1 추가
		     ===> 병합 커밋이 사라졌다.

	eunjaeui-MacBookPro:hello-git-cli eunjae$ git log --oneline --graph --all -n3   # 로그 확인
		---> * 209e069 (origin/master, master, hotfix) hotfix 실습
		     | * c259819 (HEAD -> feature1) 새로운 기능 1 추가
		     |/
		     * ea16908 (tag: v0.1) 두 번째 커밋
		     ===> 재배치 대상 커밋의 체크섬 값이 'c259819'라는 것을 알 수 있다.

	eunjaeui-MacBookPro:hello-git-cli eunjae$ git rebase master   # HEAD 브랜치의 커밋들을 master로 재배치
		   ---> First, rewinding head to replay your work on top of it...
			Applying: 새로운 기능 1 추가
			Using index info to reconstruct a base tree...
			M  file1.txt
			Falling back to patching base and 3-way merge...
			Auto-merging file1.txt
			CONFLICT (content): Merge conflict in file1.txt
			error: Failed to merge in the changes.
			Patch failed at 0001 새로운 기능 1 추가
			hint: Use 'git am --show-current-patch' to see the failed patch

			Resolve all conflicts manually, mark them as resolved with
			"git add/rm <conflicted_files>", then run "git rebase --continue".
			You can instead skip this commit: run "git rebase --skip".
			To abort and get back to the state before "git rebase", run "git rebase --abort". 
			===> merge에서와 마찬가지로 충돌로 인해 rebase가 실패했다. 
			===> 실패 메시지를 보면 수동으로 충돌을 해결한 후에 스테이지에 추가할 것을 알려준다.
			===> 그러고 난후 git rebase --continue 명령을 수행하라는 것도 알려준다.

	eunjaeui-MacBookPro:hello-git-cli eunjae$ git push   # 원격에 push
		   ---> fatal: You are not currently on a branch.
			To push the history leading to the current (detached HEAD)
			state now, use

				git push origin HEAD:<name-of-remote-branch>
	```
	- 따라서, 충돌을 해결하고 다시 rebase를 해보자.

- 충돌 해결 및 rebase 이어서 하기
	```
	$ git status   # 충돌 대상 확인 및 수동으로 충돌 해결
		   ---> rebase in progress; onto 209e069
			You are currently rebasing branch 'feature1' on '209e069'.
				(fix conflicts and then run "git rebase --continue")
				(use "git rebase --skip" to skip this patch)
				(use "git rebase --abort" to check out the original branch)

			Unmerged paths:
				(use "git reset HEAD <file>..." to unstage)
				(use "git add <file>..." to mark resolution)

						both modified: file1.txt

			no changes added to commit (use "git add" and/or "git commit -a")
			===> 충돌 파일을 확인하고 VSCode를 이용해서 수동으로 내용을 수정하고 저장.
			

	$ git add file1.txt   # 변경사항 스테이징 및 상태 확인

	$ git status
		   ---> rebase in progress; onto 209e069
			You are currently rebasing branch 'feature1' on '209e069'.
				(all conflicts fixed: run "git rebase --continue")

			Changes to be committed:
				(use "git reset HEAD <file>..." to unstage)

						modified: file1.txt

	$ git rebase --continue   # 리베이스 계속 진행
		   ---> Applying: 새로운 기능 1 추가
			===> merge는 마지막 단계에서 git commit 명령을 사용하지만, rebase는 git rebase --contivue 명령을 사용한다는 것에 주의하자.
	
	$ git log --oneline --graph --all -n2   # 로그 확인
		   ---> * 6cea07b (HEAD -> feature1) 새로운 기능 1 추가
			* 209e069 (origin/master, master, hotfix) hotfix 실습
			===> merge와는 달리 병합 커밋도 없고 히스토리도 한 줄로 깔끔해졌다.
			===> [feature1] 브랜치가 가리키는 커밋의 체크섬 값이 '6cea07b'로 바뀐 것을 볼 수 있다. (리베이스를 하면 커밋 객체가 바뀌기 때문)

	$ git checkout master
		   ---> Switched to branch 'master'
			Your branch is up to date with 'origin/master'.
	
	$ git merge feature1   # 빨리 감기 병합
		   ---> Updating 209e069..6cea07b
			Fast-forward
				file1.txt | 4 ++++
				1 file changed, 4 insertions(+)
			===> [master] 브랜치에서 [feature1] 브랜치로 병합한다. 
			===> 한 줄이 되었기 때문에 빨리 감기 병합을 수행한다.
	```

- 3-way 병합은 기존 커밋의 변경 없이 새로운 병합 커밋을 하나 생성한다. 따라서 충돌도 한 번만 발생한다. 충돌 수정 완료 후 git commit 명령을 수행하면 merge 작업이 완료되는 것이다.
- rebase는 재배치 대상 커밋이 여러 개일 경우 여러번 충돌이 발생할 수 있다. 또한 기존 커밋을 하나씩 단계별로 수정하기 때문에 git rebase --continue 명령으로 충돌로 인해 중단된 rebase를 재개하게 된다. 
	- 따라서 여러 커밋에 충돌이 발생했다면 충돌을 해결할 때마다 git rebase --continue 명령을 매번 입력해야 한다. 
	- 복잡해지고 귀찮기 때문에 이런 경우에는 병합을 수행하는 것이 더 간단할 수 있다.

|  | 3-way 병합 | rebase |
| - | ----------| ------ |
| 특징 | 머지 커밋 생성 | 현재 커밋들을 수정하면서 대상 브랜치 위로 재배치함 |
| 장점 | 한 번만 충돌 발생 | 깔끔한 히스토리 |
| 단점 | 트리가 약간 지저분해짐 | 여러 번 충돌이 발생할 수 있음 |
<br/>

**<merge(3-way병합)>**
```
C0  ← C1 ← C4
 ↖ C2 ← C3 ↙
 
 C4에서 한 번의 충돌 발생.
   ```   

**<rebase(재결합)>**
```
C0  ← C1 ← C2' ← C3'
⇡ 
C2 ⇠ C3

 C2'와 C3'에서 충돌 발생.
 기존의 C2와 C3커밋은 C2'와 C3'로 바뀜.
```


#### 2) 유용한 rebase의 사용법 : 뻗어나온 가지 없애기
- 불필요하게 병합 커밋이 생긴 상황을 깔끔하게 정리해보자.
	- reset --hard로 병합 커밋을 되돌리고 rebase를 사용하면 된다.
	- 불필요한 가지 커밋을 만들고 없애는 실습을 해보자.

- 보통 커밋 만들기
	```
	$ echo "master1" > master1.txt   # master1.txt  파일 생성

	$ git add master1.txt   # 스테이지에 추가

	$ git commit -m "master 커밋 1"   # 커밋
		---> [master d7efba2] master 커밋 1
			2 files changed, 1 insertion(+), 3 deletions(-)
			create mode 100644 master1.txt

	$ git push origin master   # 푸시
		   ---> Enumerating objects: 9, done.
			Counting objects: 100% (9/9), done.
			Delta compression using up to 12 threads
			Compressing objects: 100% (5/5), done.
			Writing objects: 100% (7/7), 727 bytes | 727.00 KiB/s, done.
			Total 7 (delta 0), reused 0 (delta 0)
			To https://github.com/EunJaePark/hello-git-cli.git
				209e069..d7efba2  master -> master

	$ git log --oneline -n1   # 로그 확인
		---> d7efba2 (HEAD -> master, origin/master) master 커밋 1

	$ ls   # 작업 디렉토리 상태 확인
		---> file1.txt  master1.txt
	```
	- 평범하게 커밋을 하나 생성했다.
	- 이제 reset --hard를 이용해서 한 단계 이전 커밋으로 가서 다시 커밋을 생성하면 가지가 하나 생겨날 것이다.

- 가지 커밋 만들기
	```
	$ git reset --hard HEAD~   # HEAD를 한 단계 되돌리기
		---> HEAD is now at 6cea07b 새로운 기능 1 추가
		     ===> hard reset을 이용해서 [master] 브랜치를 한 단계 되돌렸다.

	$ echo "master2" > master2.txt   # master2.txt 파일 생성

	$ git add .   # 스테이지에 추가

	$ git commit -m "master2 커밋"   # 커밋
		---> [master f02fe18] master2 커밋
			1 file changed, 1 insertion(+)
			create mode 100644 master2.txt
		      ===> master2.txt 파일을 생성하고 커밋.

	$ git log --oneline --graph --all -n3   # 로그 확인
		---> * f02fe18 (HEAD -> master) master2 커밋
		     | * d7efba2 (origin/master) master 커밋 1
		     |/
		     * 6cea07b (feature1) 새로운 기능 1 추가
		     ===> master1 커밋과 master2 커밋 모두 '6cea07b'커밋을 부모로 하는 커밋이다.
		     ===> 따라서, 그래프에서 가지가 생긴 것을 확인할 수 있다.
	```
	- 현재 상황에서 git pull을 하면 가지를 병합하기 위해서 병합 커밋이 생기고 커밋 히스토리가 지저분해질 것이다.
	-  git pull = git fetch + git merge 이기 때문.

- git pull 수행 결과
	```
	$ git pull   # git pull 수행, 머지 메시지 창은 그냥 닫으면 된다.
		   ---> Merge made by the 'recursive' strategy.
			file1.txt | 3 ---
			master1.txt | 1 +
			2 files changed, 1 insertion(+), 3 deletions(-)
			create mode 100644 master1.txt
			===> git pull 명령을 수행하면 자동으로 병합 커밋이 생성된다.
			===> 병합 커밋 생성 시 에디터가 뜨는데 그냥 닫으면 된다.

	$ git log --oneline --graph --all -n4   # 병합 커밋 생성 확인
		    ---> * ffcbc77 (HEAD -> master) Merge branch 'master' of https://github.com/EunJaePark/hello-git-cli
			 |\
			 | * d7efba2 (origin/master) master 커밋 1
			 * |  f02fe18 master2 커밋
			 |/
			 * 6cea07b (feature1) 새로운 기능 1 추가
			 ===> 병합 커밋이 생성된 것을 알 수 있다.
	```
	- 이제 병합 커밋을 되돌린 후 rebase로 가지를 없애보자.

- rebase로 가지 없애기
	```
	$ git reset --hard HEAD~	# 병합 커밋 되돌리기
		---> HEAD is now at f02fe18 master2 커밋
		     ===> 마지막 커밋이 병합 커밋이었으므로 병합되기 전 커밋으로 돌아가게 된다. 

	$ git rebase origin/master   # rebase 수행으로 현재 커밋 재배치
		---> First, rewinding head to replay your work on top of it...
		     Applying: master2 커밋
		     ===> 로컬 [master] 브랜치의 가지 커밋이 [origin/master] 브랜치 위로 재배치 된다.

	$ git log --oneline --all --graph -n3   # 로그 확인
		---> * f1ad3e2 (HEAD -> master) master2 커밋
		     * d7efba2 (origin/master) master 커밋 1
		     * 6cea07b (feature1) 새로운 기능 1 추가

	$ git push   # push
		---> Enumerating objects: 4, done.
		     Counting objects: 100% (4/4), done.
		     Delta compression using up to 12 threads
		     Compressing objects: 100% (2/2), done.
		     Writing objects: 100% (3/3), 326 bytes | 326.00 KiB/s, done.
		     Total 3 (delta 0), reused 0 (delta 0)
		     To https://github.com/EunJaePark/hello-git-cli.git
			d7efba2..f1ad3e2  master -> master
		     ===> 로그를 확인하고 origin에 푸시했다.
	```
	- 이전에 튀어나와있던 가지가 사라졌다!

#### 3) rebase 주의사항
- 원격저장소에 푸시한 브랜치는 rebase하지 않는 것이 원칙!
- 따라서, rebase와 git의 동작 원리를 잘 이해하기 전까지는 로컬저장소의 브랜치에만 적용하기를 권장한다.

#### 4) 임시 브랜치 사용하기
- 원래 작업하려던 브랜치의 커밋으로 임시 브랜치를 만들고 나면 해당 브랜치에서는 아무 작업이나 막 해도 전혀 상관없다.(데이터 손실 걱정 없음!)
	- 나중에 그 브랜치를 삭제하기만 하면 모든 내용이 원상복구 된다.
	- 임시 브랜치가 필요 없어지는 시점에 CLI에서 `git branch -D <브랜치 이름>` 명령으로 삭제할 수 있다.

- 임시 브랜치 생성 사용 및 삭제
	```
	$ git branch test feature1   # feature1 브랜치에서 임시 브랜치 생성
	
	$ git checkout test   # test 브랜치 체크아웃
		---> Switched to branch 'test'

	$ echo "아무말 대잔치" > text.txt

	$ git add .

	$ git commit -m "임시 커밋"   # 새로운 커밋 생성
		---> [test c17c01a] 임시 커밋
		     1 file changed, 1 insertion(+)
		     create mode 100644 text.txt

	$ git log --oneline --graph --all -n4   # 커밋 로그 보기
		---> * c17c01a (HEAD -> test) 임시 커밋
		     | * f1ad3e2 (origin/master, master) master2 커밋
		     | * d7efba2 master 커밋 1
		     |/
		     * 6cea07b (**feature1**) 새로운 기능 1 추가

	$ git checkout master
		---> Switched to branch 'master'
		     Your branch is up to date with 'origin/master'.

	$ git branch -D test   # 임시 브랜치 삭제	
		---> Deleted branch test (was c17c01a).

	$ git log --oneline --graph --all -n3   # 로그 확인
		---> * f1ad3e2 (HEAD -> master, origin/master) master2 커밋
		     * d7efba2 master 커밋 1
		     * 6cea07b (**feature1**) 새로운 기능 1 추가
	```
	- 임시 브랜치인 [test] 브랜치를 생성하고 커밋한 후에 다시 [master] 브랜치로 돌아가서 [text] 브랜치를 삭제한 것이다.
	- 최종적으로는 아무 작업도 남지 않았음을 볼 수 있다.
	
- commit, merge, rebase 등 다양한 작업을 미리 테스트해 보고 싶을 때 간단하게 임시 브랜치를 만들어서 사용하고 불필요해지면 삭제하는 것은 좋은 Git 활용 팁이다.
		

