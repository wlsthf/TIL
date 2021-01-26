# 배포 Matrix

### 1.server clean - 실행 



### 2.putty 

접속



### 3.winscp (SFTP)

`C:\Users\yskim\eclipse-workspace\.metadata\.plugins\org.eclipse.wst.server.core` 
	tmp-data.xml 메모장에서 경로 확인
`C:\Users\yskim\eclipse-workspace\.metadata\.plugins\org.eclipse.wst.server.core\[배포될 파일 경로]`



### 4.배포(수정)

1. ​	`cd  /[경로]/apache-tomcat-9.0.19/bin` 

2. ​	ls (파일 확인)

3. ​	서버상태 확인
   ​		`ps -ef | grep [폴더명]`

4. was 중지
   		`./shutdown.sh`
   	서버상태 확인

5. ##### 	버전관리 (파일 통째로 백업!!! or 파일명 변경해서 backkkk 꼮!!! )

6. ​	소스파일 적용

7. ​	was 가동
   ​		`./startup.sh`

8. ​	서버상태 확인

9. ​	실서버 작동 확인