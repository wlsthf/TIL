# javascript) 코드의 의존성 분리

###### 자바스크립트로 버튼을 눌렀을때 텍스트에 버튼을 누른 횟수를 표시하는 코드 모델링



1. ### 어설픈 모델링

   ```javascript
   class Text {
       constructor() {
           this.view = document.createelement('div');
           this.view = textContent = '[0]';
           document.body.append(this.view);
       }
   }
   
   class Button {
       constructor() {
           this.view = document.createElement('button');
           this.view = document.textContent = 'INCREMENT';
           document.body.append(this.view);
           
           this.clicked = 0;
           this.view.onclick = () => {
   	        this.view.textContent = `[${this.clicked++}]`;            
           }
       }
   }
   
   let text = new Text();
   let button = new Button();
   ```

   

2. ### 추상화

   - ###### 전역 스코프에 `text`라는 객체가 있을 것

   - ###### `text`는 `view`라는 객체를 속성으로 가질 것

   - `text.view`는 `textContent`라는 `String`을 속성으로 가질 것

   ##### -> 전역 스코프 사용을 자제하고, 모델을 추상화 시킨다.

   ```javascript
   class Text {
       constructor() {
           this.view = document.createElement('div');
           document.body.append(this.view);
           this.render(0);
       }
       
       render(number) {
           this.view.textContent = `[${number}]`;
       }
   }
   
   class Button {
       constructor(text) {
           this.view = document.createElement('button');
           this.view.textContent = 'INCREAMENT';
           document.body.append(this.view);
           
           this.clicked = 0;
           this.view.onclick = () => {
               text.render(this.clicked++);
           }
       }
   }
   
   let text = new Text();
   let button = new Button(text);
   ```

   ```javascript
   interface Renderable {
       void render(Number number)
   }
   
   class Button {
       constructor(Renderable renderer) {
           // ...
       }
   }
   ```

   

3. ### 확장성

   > ##### 새로운 요구사항 
   >
   > - ###### `Button`에 `Renderable`한 객체들을 여러개 연결하고 싶음

   ```javascript
   class text {
   	// ...
   }
   
   class Balls {
       constructor() {
           this.view = document.createElement('div');
           document.body.append(this.view);
       }
       
       render(number) {
           this.view.innerHTML = '';
           for ( let i = 0; i < number; i++ ) {
               let ball = document.creatElement('div');
               ball.style.background = 'red';
               ball.style.width = ball.style.height = '1em';
               ball.style.display = 'inline-block';
               this.view.appendChild(ball);
           }
       }
   }
   
   class Button {
       constructor(renderers) {
           this.view = document.createElement('button');
           this.view.textContent = 'INCREMENT';
           document.body.append(this.view);
           
           this.clicked = 0;
           this.view.onclick = () => {
               this.clicked++;
               renderers.forEach(renderer => renderer.render(this.clicked));
           }
       }
   }
   
   let text = new Text();
   let balls = new Balls();
   let button = new Button([text, balls]);
   ```

   

4. ### 동적인 참조

   ```javascript
   let text = new Text();
   let balls = new Balls();
   let button = new Button([text, balls]);
   // 를 
   let button = new Button([text, balls]);
   let text = new Text();
   let balls = new Balls();
   // 로 바꿀수 없다
   ```

   > ##### 새로운 요구사항
   >
   > - ###### `Button`을 생성하는 시점이 아니라, 생성된 이후에도 `Button`에 `Renderable`들을 연결하고 싶음

   ```javascript
   class Text {
       // ...
   }
   
   class Balls {
       // ...
   }
   
   class Button {
       constructor( renderers = [] ) {
           this.view = document.createElement('button');
           this.view.textContent = 'INCREMENT';
           document.body.append(this.view);
           
           this.clicked = 0;
           this.renderers = renderers;
           this.view.onclick = () => {
               this.clicked++;
               this.renderers.forEach(renderer => renderer.render(this.clicked));
           }
       }
       
       connect(renderer) {
           this.rederers.push(renderer);
       }
   }
   
   let text = new Text();
   let button = new Button([new Balls()]);
   button.connect(text);
   ```

   

5. ### 의존성 없애기

   > ##### 새로운 요구사항
   >
   > - `Balls, Text`를 `Renderable`에서 탈피시키며 의존성을 완전히 없애기

   ```javascript
   class Text {
     constructor(){
       this.view = document.createElement('div');
       document.body.append(this.view);
       this.number = 0;
       this.count();
     }
   
     count(){
       this.view.textContent = `[${this.number++}]`;
     }
   }
   
   class Balls {
     constructor(){
       this.view = document.createElement('div');
       document.body.append(this.view);
     }
   
     generate(){
       this.view.innerHTML = '';
       let number = Math.floor(Math.random()*10);
       for(let i=0; i<number; i++) {
         let ball = document.createElement('div');
         ball.style.background = 'orange';
         ball.style.width = ball.style.height = '1em';
         ball.style.borderRadius = '50%';
         ball.style.display = 'inline-block';
         this.view.appendChild(ball);
       }
     }
   }
   
   class Button {
     constructor(text){
       this.view = document.createElement('button');
       this.view.textContent = text;
       document.body.append(this.view);
   
       this.clickHandlers = [];
       this.view.onclick = () => {
         this.clicked++;
         this.clickHandlers.forEach(handler => handler(this.clicked));
       }
     }
   
     addClickHandler(handler) {
       this.clickHandlers.push(handler);
     }
   }
   
   let balls = new Balls();
   let text = new Text();
   
   // increment button
   let button = new Button('INCREMENT');
   button.addClickHandler(() => {
     text.count();
   });
   
   // button for both
   let button2 = new Button('CLICK ME');
   button2.addClickHandler(() => {
     balls.generate();
     text.count();
   });
   ```

   





참조 [okky - kdw](https://okky.kr/article/409329)