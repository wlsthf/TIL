# javascript ) JS를 이용한 각종 정규식 마스킹



### Email

```javascript
var OriginData = $OriginData.val();
 
var findMasking = "*";
var ContentsData;
var len;
 
 
                //email masking
                var emailsArray = OriginData.match(/([a-zA-Z0-9._-]+@[a-zA-Z0-9._-]+\.[a-zA-Z0-9._-]+)/gi);
 
                if(emailsArray== null || emailsArray =="")
                {
                    ContentsData = OriginData;
                }
                else
                {
                    len = emailsArray.toString().split('@').length;
                    ContentsData = OriginData.toString().replace(new RegExp('.(?=.{0,' + len + '}@)', 'g'), '*');
                }
 
 
// email1234@daum.net
// email1***@daum.net
```





### Card

```javascript
  // card  masking _16
                var cardArray = ContentsData.match(/(\d{4})-(\d{4})-(\d{4})-(\d{4})/gi);
                if(cardArray== null || cardArray =="")
                {
                    ContentsData = ContentsData;
                }
                else
                {
                  for (var i = 0; i <cardArray.length ; i++)
                  {
                    ContentsData = ContentsData.toString().replace(cardArray[i],cardArray[i].toString().replace(/(\d{4})-(\d{4})-(\d{4})-(\d{4})/gi,"$1-****-****-$4"));
                    }
                }
 
                cardArray = ContentsData.match(/(5[1-5]\d{14})|(4\d{12})(\d{3}?)|3[47]\d{13}|(6011\d{12})/gi);
                if(cardArray== null || cardArray =="")
                {
                    ContentsData = ContentsData;
                }
                else
                {
                    
                   for (var i = 0; i <cardArray.length ; i++)
                  {
                    ContentsData = ContentsData.toString().replace(cardArray[i],cardArray[i].toString().replace(/(\d{4})(\d{4})(\d{4})(\d{4})/gi,"$1********$4"));
                    }
                }
 

// 4000-1234-5678-0000
// 4000-****-****-0000

```





### 주민등록번호

```javascript
// National identification Number masking_13
                var ninArray = ContentsData.match(/(?:[0-9]{2}(?:0[1-9]|1[0-2])(?:0[1-9]|[1,2][0-9]|3[0,1]))-[1-4]{1}[0-9]{6}\b/gi);
                if(ninArray== null || ninArray =="")
                {
                    ContentsData = ContentsData;
                }
                else
                {
                    len = ninArray.toString().split('-').length;
                    ContentsData = ContentsData.toString().replace(ninArray,ninArray.toString().replace(/-?([1-4]{1})([0-9]{5})$/gi,"******"));
                }
 
                ninArray = ContentsData.match(/\d{13}/gi);
                if(ninArray== null || ninArray =="")
                {
                    ContentsData = ContentsData;
                }
                else
                {
                    ContentsData = ContentsData.toString().replace(ninArray,ninArray.toString().replace(/([0-9]{6})$/gi,"******"));
                }

// 000101-1234567
// 000101-1******
```





### 전화번호

```javascript
// phone masking_11
                var phoneArray = ContentsData.match(/\d{2,3}-\d{3,4}-\d{4}/gi);
 
                if(/-[0-9]{3}-/.test(phoneArray))
                { // 00-000-0000 형태인 경우
                    for (var i = 0; i <phoneArray.length ; i++) {
                        alert(phoneArray[i]);
                    ContentsData= ContentsData.toString().replace(phoneArray[i],phoneArray[i].toString().replace(/-[0-9]{3}-/g, "-***-"));
                    }
                }
                else if(/-[0-9]{4}-/.test(phoneArray))
                { // 00-0000-0000 형태인 경우
                    for (var i = 0; i <phoneArray.length ; i++) {
                        alert(phoneArray[i]);
 
                    ContentsData= ContentsData.toString().replace(phoneArray[i],phoneArray[i].toString().replace(/-[0-9]{4}-/g, "-****-"));
                    }
                }
 
 
 
                phoneArray = ContentsData.match(/\d{11}/gi);
 
                if(phoneArray== null || phoneArray =="")
                {
                    ContentsData = ContentsData;
                }
                else
                {
 
 
                    ContentsData = ContentsData.toString().replace(phoneArray[i],phoneArray[i].toString().replace(/(\d{3})(\d{4})(\d{4})/gi,'$1****$3'));
 
                }


// 010-0000-0000
// 010-****-0000

```





### 계좌번호

```javascript
// account Masking_10
                var accountArray = ContentsData.match(/\d{10}/gi);
                alert(accountArray);
                if(accountArray== null || accountArray =="")
                {
                    ContentsData = ContentsData;
                }
                else
                {
                    ContentsData = ContentsData.toString().replace(accountArray,accountArray.toString().replace(/([0-9]{6})$/gi,'******'));
                }
 
 
                // car masking_11
                var accountArray = ContentsData.match(/[0-9]{2}[가~힣]{1}[\s]*[0-9]{4}/gi);
                alert(accountArray);
                if(accountArray== null || accountArray =="")
                {
                    ContentsData = ContentsData;
                }
                else
                {
                    ContentsData = ContentsData.toString().replace(accountArray,accountArray.toString().replace(/([0-9]{6})$/gi,'******'));
                }

```



출처 : [빛나는 리오a 티스토리](https://rios.tistory.com/entry/JS-Javascirpt-%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EA%B0%81%EC%A2%85-%EC%A0%95%EA%B7%9C%EC%8B%9D%EB%A7%88%EC%8A%A4%ED%82%B9-%EB%B0%A9%EB%B2%95?category=711004)

