## `git pull --rebase`

- `git pull --rebase` 명령어를 이용해 리베이스하려 했으나 아래와 같은 오류가 날 경우 `--abort`를 해준 후 다시 rebase를 해준다.

    ```
    $ git pull --rebase origin dev
    ```
    ```
     * branch            dev        -> FETCH_HEAD
    fatal: It seems that there is already a rebase-merge directory, and
    I wonder if you are in the middle of another rebase.  If that is the
    case, please try
            git rebase (--continue | --abort | --skip)
    If that is not the case, please
            rm -fr ".git/rebase-merge"
    and run me again.  I am stopping in case you still have something
    valuable there.
    ```
    ```
    $ git rebase --abort
    ```
    
    > `$ git reset --hard origin/feat/license`를 해주면 마지막으로 원격브랜치에 push했던 부분으로 해당 브랜치가 리셋된다. 

- `conflict`이 발생한 내용들을 수정해준 후, staging해준다. 
    ```
    $ git add --all 
    ```
    `git add --all`은 root부터 변경된 모든 사항을 스테이징하는 반면, `git add .`은 현재 해당하는 부분만 스테이징 된다.
    
- `rebase`는 순서대로 변경된 부분들을 해결하기 때문에, 모든 충돌사항을 수정할 수 있도록 스테이징 후 `continue`를 해줘야 한다.
    ```
    $ git rebase --continue
    ```
    
    
- 모든 conflict이 해결되면 현재 브랜치가 가장 최신버전이라는 안내가 나온다.
   ```
   https://gitlab.accordions.co.kr/accordion/v2/front/console URL에서
    * branch            dev        -> FETCH_HEAD
   Current branch feat/license is up to date.
   ```
   
- conflict이 모두 해결되면 원격브랜치로 push를 해준다.
  ```
  $ git push origin feat/license
  ```
  그러나 원격브랜치에 변경사항이 있을 경우 push가 실패하고 아래와 같은 메세지가 보일 것이다.
  ```
  husky > pre-push (node v14.16.0)

  > accordion-web@0.0.29 eslint /Users/pej/Desktop/회사폴더/console
  > eslint --ext .ts .


  /Users/pej/Desktop/회사폴더/console/src/stores/events/store-events.ts
    55:29  warning  'event' is defined but never used. Allowed unused args must match /^_/u  @typescript-eslint/no-unused-vars

  ✖ 1 problem (0 errors, 1 warning)

  To https://gitlab.accordions.co.kr/accordion/v2/front/console.git
   ! [rejected]        feat/license -> feat/license (non-fast-forward)
  error: 레퍼런스를 'https://gitlab.accordions.co.kr/accordion/v2/front/console.git'에 푸시하는데 실패했습니다
  힌트: 현재 브랜치의 끝이 리모트 브랜치보다 뒤에 있으므로 업데이트가
  힌트: 거부되었습니다. 푸시하기 전에 ('git pull ...' 등 명령으로) 리모트
  힌트: 변경 사항을 포함하십시오.
  힌트: 자세한 정보는 'git push --help'의 "Note about fast-forwards' 부분을
  힌트: 참고하십시오.
  ```
  
  이 경우, 강제 push를 해준다. 
  (단, 개인적으로 사용하는 브랜치일 때만 강제 push를 해도 된다.)
  ```
  $ git push origin +feat/license
  ```
  `+`는 `hard`의 줄임표현이다.
  
  
- 강제 push가 되면 아래와 같은 메세지를 볼 수 있다.
  ```
  husky > pre-push (node v14.16.0)

  > accordion-web@0.0.29 eslint /Users/pej/Desktop/회사폴더/console
  > eslint --ext .ts .


  /Users/pej/Desktop/회사폴더/console/src/stores/events/store-events.ts
    55:29  warning  'event' is defined but never used. Allowed unused args must match /^_/u  @typescript-eslint/no-unused-vars

  ✖ 1 problem (0 errors, 1 warning)

  오브젝트 나열하는 중: 96, 완료.
  오브젝트 개수 세는 중: 100% (96/96), 완료.
  Delta compression using up to 8 threads
  오브젝트 압축하는 중: 100% (72/72), 완료.
  오브젝트 쓰는 중: 100% (78/78), 11.15 KiB | 308.00 KiB/s, 완료.
  Total 78 (delta 49), reused 0 (delta 0), pack-reused 0
  remote: 
  remote: View merge request for feat/license:
  remote:   https://gitlab.accordions.co.kr/accordion/v2/front/console/-/merge_requests/68
  remote: 
  To https://gitlab.accordions.co.kr/accordion/v2/front/console.git
   + 58bd855...cecc22d feat/license -> feat/license (forced update)
  ```
  
  
  
