中文參考
https://developer.mozilla.org/zh-TW/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Angular_getting_started
Angular lesson
https://angular.io/tutorial/first-app/first-app-lesson-11
Module
https://www.stevenchang.tw/blog/2019/07/31/Angular_module_basic_note
Import Http Client
private http: HttpClient;
this.http.get(this.url);
…
https://www.telerik.com/blogs/angular-basics-how-to-use-httpclient





Angular 
Security
https://angular.io/guide/security



Angular 是一個基於TypeScript的開發平台。身為一個平台，Angular 包含：
* 一個元件化的框架，用來建構可延展的 Web 應用程式。
* 一整套經深思熟慮而整合出來的函式庫，包含各種不同的功能，包含路由機制、表單管理、Client/Server 通訊，以及更多。
* 一組完善的開發工具，幫助你開發、建置、測試、更新你的程式碼。


Angular CLI 是一種快速、簡單、備受推崇的 Angular 程式開發方式。
ng build	編譯Angular開發的程式到輸出目錄
ng serve	建構應用程式並啟動開發伺服器，當檔案變化時重新建構
ng generate	根據原理圖去生成或修改檔案
ng test	對指定專案進行單元測試
ng e2e	編譯並啟動Angular程式，並執行端到端測試


前置
Node.js
npm 套件管理器

npm install -g @angular/cli

ng new todo --routing=false --style=css

npm start
 will run whatever you have defined for the start command of the scripts object in your package.json file.
"scripts": {
  "start": "ng serve"
}

[npm]解決安裝npm套件時遇到Conflicting peer dependency 
npm install --legacy-peer-deps




src/app
其它json
1. app.module.ts：列出此專案使用的所有檔案。此檔案在專案中扮演中央樞紐的角色。
2. app.component.ts：又被稱為元件類別（Class），內含此專案主要頁面的相關邏輯
3. app.component.html：內含AppComponent所使用的網頁 html。這個檔案的內容也被視為元件模板（Template），此模板定義你在瀏覽器中看到的畫面。
4. app.component.css：內含AppComponent裡面的樣式。當你想定義某些樣式給特定模組使用，卻不希望影響到整體程式時，便可使用此檔案進行設定。
5. 測試類別app.component.spec.ts


@Component() 裝飾器
裡面會有檔案的路徑指向，告訴 Angular 要去哪裡找 HTML 和 CSS 檔案
還有Selector給要引用此component的html的標籤


<h1>{{ title }}</h1>
Angular 會自動重新渲染該節點
Angular是一个典型的MVVM框架，
* 模型(Model)：模型和MVC模式中的模型是一样的，它是应用程序的数据结构。
* 视图(View)：视图也和MVC模式中的视图是一样的，它是用户看到的界面。
* 视图模型(ViewModel)：视图模型是视图的抽象，它不仅包含视图的状态和行为，还包含了业务逻辑。视图模型通过双向数据绑定与视图进行通信，这样当模型的数据改变时，视图会自动更新。
很多情況Component就是ViewModel

Anguar 的理念是想要透過數據綁定來消除傳統的 DOM 操作，進而減少複雜的操作以及避免錯誤的產生。

MVC和MVVM模式都是为了将用户界面和业务逻辑分离，使得代码更易于维护和扩展。



	Angular package https://angular.io/guide/npm-packages
package.json
PACKAGES	DETAILS
Dependencies	Essential to running applications.
DevDependencies	Only necessary to develop and build applications.
common >> 有http
core >> component, dependency injection
router >> …
@angular/platform-browser	Everything DOM and browser related, especially the pieces that help render into the DOM. This package also includes the bootstrapModuleFactory() method for bootstrapping applications for production builds that pre-compile with AOT.
@angular/platform-browser-dynamic	Includes providers and methods to compile and run the application on the client using the JIT compiler.
rxjs >> observable
zone.js >> javascript

tsconfig又是跟test相關的

package-lock.json
It stores an exact, versioned dependency tree rather than using starred versioning like package.json itself (e.g. 1.0.*). This means you can guarantee the dependencies for other developers or prod releases, etc. It also has a mechanism to lock (hence the name package-lock) the tree but generally will regenerate if package.json changes.
https://stackoverflow.com/questions/44297803/what-is-the-role-of-the-package-lock-json


~
In the simplest terms, the tilde matches the most recent minor version (the middle number).
~1.2.3 will match all 1.2.x versions but will miss 1.3.0.

^
It will update you to the most recent major version (the first number). ^1.2.3 will match any 1.x.xrelease including 1.3.0, but will hold off on 2.0.0.




Angular App 主要由這八個元素構成：
￼
Data binding https://hackmd.io/@Heidi-Liu/angular-data-binding
￼

Template Driven Forms 與 Reactive Forms https://ithelp.ithome.com.tw/articles/10275677
模板式 VS 響應式(更重視響應 與 測試)
	Reactive Forms	Template Driven Forms
表單模型的設置	清楚的，在 Component 裡建立	隱晦的，用 Directive 建立
資料模型	有結構性且不變的	鬆散且容易改變
可預測性	同步的	非同步的
表單驗證方式	用函式驗證	用 Directive 驗證




Dependency Inject
>> 降低模組間的依賴度 彈性 抽換 >> angular只是提供了更好的DI實作語法





Then  Promise

function consoleWrite(line:string) { console.log(line); }

const p = async () : Promise<string | string> => {
    const data = new Promise<string | string>((resolve, reject) => {
        setTimeout(() => {
            let num:number = 3; num >= 3 ? resolve('成功') : reject('失敗');
        }, 3000);
    });
    consoleWrite('等待 ...');
    await data;
    return data;
};

p().then((res) => consoleWrite(res)); // p.then(consoleWrite);
p().catch(err => { console.log(err); throw err; }); // thow if neccessary
p().finally();




Observale

import { Observable } from 'rxjs'; import { of, map, catchError } from 'rxjs';
const obs = new Observable((subscriber) => { subscriber.next(3); })
.pipe(
  map(num => { if (num >= 3) { return '成功'; } else { throw new Error('失敗'); } }),
  catchError(err => { throw new Error('失敗'); })
);
obs.subscribe( res => console.log(res), err => console.log(err), () => console.log('結束') );

numbers$.subscribe({
  next: value => console.log('Observable emitted the next value: ' + value),
  error: err => console.error('Observable emitted an error: ' + err),
  complete: () => console.log('Observable emitted the complete notification')
});
或是
  next: value => console.log('Observable emitted the next value: ' + value),
  error: err => console.error('Observable emitted an error: ' + err),

Observable 部分
https://angular.io/guide/observables

Observable
FromEvent
https://rxjs.dev/api/index/function/fromEvent

Observable比較優勢
https://angular.io/guide/comparing-observables

Observable跟promise
兩者可以混用
https://segmentfault.com/a/1190000042528145

更多特殊用途 container https://reactivex.io/rxjs/manual/overview.html#behaviorsubject 

import { BehaviorSubject } from 'rxjs';
var subject = new BehaviorSubject(0); // 0 is the initial value
subject.subscribe({  next: (v) => console.log('observerA: ' + v)});
subject.next(1);subject.next(2);
subject.subscribe({ next: (v) => console.log('observerB: ' + v) });subject.next(3);


OPERATION	OBSERVABLE	PROMISE
Creation	new Observable((observer) => { 
  observer.next(123); 
});	new Promise((resolve, reject) => { 
  resolve(123); 
});
Transform	obs.pipe(map((value) => value * 2));	promise.then((value) => value * 2);
Subscribe	sub = obs.subscribe((value) => { 
  console.log(value) 
});	promise.then((value) => { 
  console.log(value); 
});
Unsubscribe	sub.unsubscribe();	Implied by promise resolution.

	OBSERVABLE	EVENTS API
Creation & cancellation	// Setup 
const clicks$ = fromEvent(buttonEl, 'click'); 
// Begin listening 
const subscription = clicks$ 
  .subscribe(e => console.log('Clicked', e)) 
// Stop listening 
subscription.unsubscribe();	function handler(e) { 
  console.log('Clicked', e); 
} 
// Setup & begin listening 
button.addEventListener('click', handler); 
// Stop listening 
button.removeEventListener('click', handler);
Subscription	observable.subscribe(() => { 
  // notification handlers here 
});	element.addEventListener(eventName, (event) => { 
  // notification handler here 
});
Configuration	Listen for keystrokes, but provide a stream representing the value in the input.
      
      
fromEvent(inputEl, 'keydown').pipe( 
  map(e => e.target.value) 
);	Does not support configuration.
      
      
element.addEventListener(eventName, (event) => { 
  // Cannot change the passed Event into another 
  // value before it gets to the handler 
});


Unit test 詳解
https://medium.com/simform-engineering/how-to-write-unit-tests-with-jasmine-karma-f1908bdeb617
Karma = Test runner (testing environment):
快速建構及執行 test code 的環境工具，常見的有: Karma / Jest / Chai 等等… 官方內建的是 Karma。
Jasmine = Assertion library (斷言庫):
輔助 Test runner 對錯判定的工具，通常有很多好用的 method 幫助做比對，常見的有: Jasmine / Enzyme / Mocha 等等… 官方內建的是 Jasmine。
以上提到的 Karma & Jasmine 兩者都已內建，通常不必再另外裝

執行 Karma 的用法，跟我們熟知使用 library 的方式差不多
，一樣是在 package.jason 添加腳本並運行，例如常見的 run test
"test": "ng test"




一開始，的確是叫做 AngularJS 沒錯！
直到後來大版號升上 2 之後，才正式將其正名為 Angular ，
以便可以跟 1.x 版的 AngularJS 區分開來。而且 1.x 版的 AngularJS 其實還算是函式庫，
