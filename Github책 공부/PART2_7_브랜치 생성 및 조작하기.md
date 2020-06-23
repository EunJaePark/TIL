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
- 
