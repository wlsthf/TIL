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

5. ## Hotfix Branch



출처:[Heee's Development Blog](https://gmlwjd9405.github.io/2018/05/11/types-of-git-branch.html)