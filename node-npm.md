---
title: node npm
categories:
  - npm
  - node
tags:
  - npm
  - node
toc: true
---

# node npm

npm install -h: isntall할 때 쓸 수 있는 명령어 list

ex\) “bcrypt”: “^0.8.3" ::  
^를 입력하면 major release를 바꾸지 않고 최대한 \(minor release를 최대한 Update ~0.8.3이라고 써져있다면 patch release만 최대한 update 하겠다는 의미

`-g` `--save` `--dev`

npm update 전부 업데이트한다.\(~와 ^가 있을때만.\) nam update moduleName으로 특정 module만 업데이트 하는 것도 가능 nam update moduleName -g라고 하면 무조건 major release 최신 버전으로 업데이트 된다.

npm uninstall packageName 이 명령어만으로는 package.json에서 없어지지 않는다. npm uninstall packageName —save 라고 쓴다면, package.json에서도 없어지게 될 것이다. npm uninstall mocha —save-dev\(devDependancy 부분을 package.json에서 삭제한다.\) npm uninstall packageName -g global 레벨에서 페키지를 지웠다.

Ex\) jquery, bootstrap js

```javascript
package.json
    "devDependencies": { 
"jquery": "~3.1.0", 
"bootstrap": "~3.3.7", 
}
```

npm install copy: node\_modules에 존재하는 Bootstrap의 배포 파일\(CSS, 글꼴, 이미지 등\)을 지정한 경로에 복사 사용 -&gt; 

