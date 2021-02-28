

## HTML FORM 사용

-  **회원** 목록 /members **-> GET** •
-  **회원** 등록 폼 /members/new **-> GET** •
-  **회원** 등록 /members/new, /members **-> POST** •
-  **회원** 조회 /members/{id} **-> GET** • 
- **회원** 수정 폼 /members/{id}/edit **-> GET** •
-  **회원** 수정 /members/{id}/edit, /members/{id} **-> POST** •
-  **회원** 삭제 /members/{id}/delete **-> POST****HTML FORM** **사용** 



- HTML FORM은 **GET, POST**만 지원

-  **컨트롤** **URI** 

  -  GET, POST만 지원하므로 제약이 있음 

  - 이런 제약을 해결하기 위해 동사로 된 리소스 경로 사용 

  -  POST의 /new, /edit, /delete가 컨트롤 URI 

  - HTTP 메서드로 해결하기 애매한 경우 사용(HTTP API 포함)

    

## 정리

-  **HTTP API -** **컬렉션** **•** **POST** **기반 등록** **•** **서버가 리소스** **URI** **결정** **•** **HTTP API -** **스토어** **•** **PUT** **기반 등록** **•** **클라이언트가 리소스** **URI** **결정** • **HTML FORM** **사용** • 순수 HTML + HTML form 사용 • GET, POST만 지원
- 
- 



## 정리 **참고하면 좋은** **URI** **설계 개념**

 **•** **문서****(document)**  

​	• 단일 개념(파일 하나, 객체 인스턴스, 데이터베이스 row) 

​	• 예) /members/100, /files/star.jpg

**•** **컬렉션****(collection)**  

​	• 서버가 관리하는 리소스 디렉터리

​	• 서버가 리소스의 URI를 생성하고 관리 

​	• 예) /members

**•** **스토어****(store)**  

​	• 클라이언트가 관리하는 자원 저장소 

​	• 클라이언트가 리소스의 URI를 알고 관리

​	• 예) /files 

**•** **컨트롤러****(controller),** **컨트롤** **URI**  

​	• 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스 실행

​	• 동사를 직접 사용 • 예) /members/{id}/delete 

- 



https://restfulapi.net/resource-naming



