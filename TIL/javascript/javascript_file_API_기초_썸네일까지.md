# javascript) file API  기초 - 썸네일까지

### 참조 : [FileReader](https://caniuse.com/filereader)



## 텍스트 파일 읽기

```html
<pre id="preview">텍스트 파일 내용 출력 영역</pre>
<input type="file" id="getfile" accept="text/*">
<!--텍스트 파일만-->

<script>
	var file = document.getElementById("getfile");
    
    file.onchange = function() {
        var fileList = file.files;
        
        // 읽기
        var reader = new FileReader();
        reader.readAsText(fileList[0]);
        
        // 로드 한 후
        reader.onload = function() {
            document.getElementById("preview").textContent = reader.result;
        }
    }
</script>
```





## 이미지 파일 읽기

```html
<img id="preview" src="" width="700" alt="로컬에 있는 이미지가 보여지는 영역">
<input type="file" id="getfile" accept="image/*">

<script>
    var file = document.getElementById("getfile");
    
	file.onchange = function() {
        var fileList = file.files;
        
        // 읽기
        var reader = new FileReader();
        reader.readAsDataURL(fileList.get(0));
        
        // 로드 한 후
        reader.onload = function() {
            document.getElementById("preview").src = reader.result;
        }
    }
</script>
```





## 이미지의 썸네일 만들기

```html
<img id="preview" src="" width="700" alt="로컬에 있는 이미지가 보여지는 영역">
<a id="download" download="thumbnail.jpg" target="_blank">
    <img id="thumbnail" src="" width="100" alt="썸네일영역 (클릭하면 다운로드 가능)">
</a>
<input type="file" id="getfile" accept="image/*">

<script>
	var file = document.getElementById('getfile');
    
    file.onchange = function() {
        var fileList = file.files;
        
        // 읽기
        var reader = new FileLeader();
        reader.readAsDataURL(fileList[0]);
        
        // 로드 한 후
        reader.onload = function() {
            // 로컬 이미지를 보여주기
            document.getElementById('preview').src = reader.result;
            
            // 썸네일 이미지 생성
            var tmpImg = new Image();
            tmpImg.src = reader.result;
            tmpImg.onload = function() {
                // 리사이즈를 위해 캔버스 객체 생성
                var canvas = document.createElement('canvas');
                var canvasContext = canvas.getContext('2d');
                
                // 캔버스 크기 설정
                canvas.width = 100;
                canvas.heigth = 100;
                
                // 이미지를 캔버스에 그리기
                canvasContext.drawImage(this, 0, 0, 100, 100);
                
                // 캔버스에 그린 이미즐 다시 data-uri 형태로 변환
                var dataURI = canvas.toDataURL('image/jpeg');
                
                // 썸네일 이미지 보여주기
                document.getElementById('thumbnail').src = dataURI;
                
                // 썸네일 이미지를 다운로드할 수 있도록 링크 설정
                document.querySelector('#download').herf = dataURI;
            }
        }
    }
</script>
```

출처: [감성 프로그래밍](https://programmingsummaries.tistory.com/367)

