# git) Git Branch 종류 및 사용법 ( 5가지 )

## Goal

> - ##### `Gitflow Workflow`에서 사용하는 `Git Branch` 종류를 이해한다.
>
> - ##### `Gitflow Workflow`에서 사용하는 `Git Branch` 사용법을 이해한다.

## Git Branch 종류 ( 5가지 )

###### `Gitflow Workflow`에서는 항상 유지되는 메인 브랜치들(`master, develop`)과 일정 기간 동안만 유지되는 보조 브랜치들 (`feature, release, hotfix`)을 포함하여 총 5가지의 브랜치를 사용한다.



1. ## Master Branch

   #### 제품으로 출시될 수 있는 브랜치

   ###### 배포(Release) 이력을 관리하기 위해서 사용. 즉, 배포 가능한 상태만을 관리한다.

   

2. ## Develop Branch

   #### 다음 출시 버전을 개발하는 브랜치

   ###### 기능 개발을 위한 브랜치들을 병합하기 위해 사용. 즉, 모든 기능이 추가되고 버그가 수정되어 배포 가능한 안정적인 상태라면 develop 브랜치를 master브랜치에 merge한다.

   ###### 평소에는 이 브랜치를 기반으로 개발을 진행한다.

   

3. ## Feature branch

   #### 기능을 개발 하는 브랜치

   ###### feature 브랜치는 새로운 기능 개발 및 버그 수정이 필요할 때마다 develop 브랜치로 부터 분기한다. feature 브랜치에서의 작업은 기본적으로 공유할 필요가 없기 때문에, 자신의 로컬 저장소에서 관리한다. 

   ###### 개발이 완료되면 develop브랜치로 merge하여 다른사람들과 공유한다.

   1. ###### develop 브랜치에서 새로운 기능에 대한 feature 브랜치를 분기한다.

   2. ###### 새로운 기능에 대한 작업을 수행한다.

   3. ###### 작업이 끝나면 develop브랜치로 merge 한다.

   4. ###### 더 이상 필요하지 않은 feature 브랜치는 삭제한다.

   5. ###### 새로운 기능에 대한 feature 브랜치를 중앙 원격 저장소에 올린다.

   

   - ##### feature 브랜치 이름 정하기

     - ###### master, develop, release-(RB_), of hotfix- 제외

     - ###### [feature/기능요약] 형식을 추천 EX) feature/login

   - ##### feature 브랜치 생성 및 종료 과정

     ```bash
     // feature 브랜치(feature/login)를 'develop' 브랜치('master' 브랜치에서 따는 것이 아니다!)에서 분기
     $ git checkout -b feature/login develop
     
     /* ~ 새로운 기능에 대한 작업 수행 ~ */
     
     /* feature 브랜치에서 모든 작업이 끝나면 */
     // 'develop' 브랜치로 이동한다.
     $ git checkout develop
     // 'develop' 브랜치에 feature/login 브랜치 내용을 병합(merge)한다.
     # --no-ff 옵션: 아래에 추가 설명
     $ git merge --no-ff feature/login
     // -d 옵션: feature/login에 해당하는 브랜치를 삭제한다.
     $ git branch -d feature/login
     // 'develop' 브랜치를 원격 중앙 저장소에 올린다.
     $ git push origin develop
     ```

   - ##### --no-ff 옵션

     - ###### 새로운 커밋 객체를 만들어 develop 브랜치에 merge 한다.

     - ###### 이것은 feature 브랜치에 존재하는 커밋 이력을 모두 합쳐서 하나의 새로운 커밋 객체를 만들어 develop 브랜치로 merge하는 것이다.

   

4. ## Release Branch

   ###### 이번 출시 버전을 준비하는 브랜치

   ###### 배포를 위한 전용 브랜치를 사용함으로써 한 팀이 해당 배포를 준비하는 동안 다른 팀은 다음 배포를 위한 기능 개발을 계속할 수 있다. 즉, 딱딱 끊어지는 개발 단계를 정의하기에 아주 좋다.

   ###### 예를 들어, ‘이번 주에 버전 1.3 배포를 목표로 한다!’라고 팀 구성원들과 쉽게 소통하고 합의할 수 있다는 말이다.

   ###### ‘develop’ 브랜치에서 배포할 수 있는 수준의 기능이 모이면 또는 정해진 배포 일정이 되면, release 브랜치를 분기한다.

   ###### release 브랜치를 만드는 순간부터 배포 사이클이 시작된다.

   ###### release 브랜치에서는 배포를 위한 최종적인 버그 수정, 문서 추가 등 릴리스와 직접적으로 관련된 작업을 수행한다.

   ###### 직접적으로 관련된 작업들을 제외하고는 release 브랜치에 새로운 기능을 추가로 병합(merge)하지 않는다.

   ###### ‘release’ 브랜치에서 배포 가능한 상태가 되면(배포 준비가 완료되면),

   ###### 배포 가능한 상태: 새로운 기능을 포함한 상태로 모든 기능이 정상적으로 동작 하는 상태

   ###### ‘master’ 브랜치에 병합한다. (이때, 병합한 커밋에 Release 버전 태그를 부여!)

   ###### 배포를 준비하는 동안 release 브랜치가 변경되었을 수 있으므로 배포 완료 후 ‘develop’ 브랜치에도 병합한다.

   ###### 이때, 다음 번 배포(Release)를 위한 개발 작업은 ‘develop’ 브랜치에서 계속 진행해 나간다.

   

   ##### release 브랜치 이름 정하기

   ###### 	release-RB_* 또는 release-* 또는 release/* 처럼 이름 짓는 것이 일반적인 관례

   ###### 	[release-* ] 형식을 추천 EX) release-1.2

   

   ##### release 브랜치 생성 및 종료 과정

   ```bash
   // release 브랜치(release-1.2)를 'develop' 브랜치('master' 브랜치에서 따는 것이 아니다!)에서 분기
   $ git checkout -b release-1.2 develop
   
   /* ~ 배포 사이클이 시작 ~ */
   
   /* release 브랜치에서 배포 가능한 상태가 되면 */
   // 'master' 브랜치로 이동한다.
   $ git checkout master
   // 'master' 브랜치에 release-1.2 브랜치 내용을 병합(merge)한다.
   # --no-ff 옵션: 위의 추가 설명 참고
   $ git merge --no-ff release-1.2
   // 병합한 커밋에 Release 버전 태그를 부여한다.
   $ git tag -a 1.2
   
   /* 'release' 브랜치의 변경 사항을 'develop' 브랜치에도 적용 */
   // 'develop' 브랜치로 이동한다.
   $ git checkout develop
   // 'develop' 브랜치에 release-1.2 브랜치 내용을 병합(merge)한다.
   $ git merge --no-ff release-1.2
   // -d 옵션: release-1.2에 해당하는 브랜치를 삭제한다.
   $ git branch -d release-1.2
   ```

   

5. ## Hotfix Branch



출처:[Heee's Development Blog](https://gmlwjd9405.github.io/2018/05/11/types-of-git-branch.html)