---
title: phpstorm
categories:
  - phpstorm
tags:
  - phpstorm
toc: true
---

# phpstorm

## codeception

### install

* with composer:  codeception/codeception --dev
* install test: with terminal, vender/bin/codecept  

### creates configuration file "codeception.yml" and tests directory

* with terminal: run **codecept  bootstrap**
* **/tests** folder you will have three .yml config files and three directories with names corresponding to these suites: unit, functional, acceptance

tests/acceptance.suite.yml  
tests/functional.suite.yml  
tests/unit.suite.yml

### create unit test \(class...\)

* run **condecept generate:test unit filename** : class name

  **!!! must run project root folder** \(ex. c:\xampp\htdocs\project1\)

  -&gt; tests folder and codeception.yml will be created under root

* under /tests/unit filenameTest.php : classnameTest.php

### Run test

* run all: use **edit configuration** 
* run each: **run**

### create acceptance test

* run **condecept generate:test acceptance Index** \(page name...\)
* IndexTest.php

  ```php
  $this->tester->amOnPage('index.php');
  $this->tester->see('xxx');
  $this->tester->fillField('username','Mike');
  // or actor class, below
  public function frontpageWorks(AcceptanceTester $I)
  {
      $I->amOnPage('/');
      $I->see('Home');  
  }
  ```

actor: AcceptanceTester  
modules:

* PhpBrowser:  

  enabled:  

  url: [http://localhost/myapp/](http://localhost/myapp/)  

  * \Helper\Acceptance  

to create actor class\(AcceptanceTester\), run build command php vendor/bin/codecept build == if not created automatically

to create test Cest file  
CODECEPT GENERATE:CEST ACCEPTANCE FIRST

test file  
tests/acceptance/FirstCest.php

```php
class FirstCest 
{
    public function frontpageWorks(AcceptanceTester $I)
    {
        $I->amOnPage('/');
        $I->see('Home');  
    }
}
```

​  
run test  
codecept run  
codecept run acceptance --steps

## Xdebug setting

php.ini and download dll

\[XDebug\] zend\_extension="c:\xampp\php\ext\php\_xdebug-2.4.0rc3-7.0-vc14.dll" xdebug.profiler\_append=0 xdebug.profiler\_enable=0 xdebug.profiler\_enable\_trigger=0 xdebug.profiler\_output\_dir="c:\xampp\tmp" xdebug.profiler\_output\_name="cachegrind.out.%t-%s" xdebug.remote\_enable=1 xdebug.remote\_handler="dbgp" xdebug.remote\_host="127.0.0.1" xdebug.remote\_log="c:\xampp\tmp\xdebug.txt" xdebug.remote\_port=9000 xdebug.trace\_output\_dir="c:\xampp\tmp" ; 3600 \(1 hour\), 36000 = 10h xdebug.remote\_cookie\_expire\_time=36000

## Inspection

Php Inspections \(EA Extended\): need to install??

* architecture related issues  - weak types control and possible code construct simplifications  - performance issues  - non-optimal, duplicate and suspicious "if" conditions  - validation of magic methods usage  - regular expressions  - validation of exception handling workflow  - compatibility issues  - variety of time-consuming bugs  - PhpUnit API usage  - security issues  
* **Alt + Shift + I** to **inspect current file** with current profile  

  **Ctrl + Alt + Shift + I** to **run inspection by name**  

  **Ctrl + Shift + F4** to **close results** of inspection.  

## Shortcut keys

* To show separator lines between methods in the editor, open the editor settings and select the Show method separators check box in the Appearance page.
* view Ctrl+Q \(View \| Quick Documentation\), Ctrl+P \(View \| Parameter Info\), Ctrl+Shift+I \(qucik definition window\) Ctrl+B \|\| Ctrl+click \(go to Declaration definition, brief info, tool tip\) Ctrl+N \(go to class\) and others can be used not only in the editor but in the code completion popup list as well.
* go to Ctrl+B \|\| Ctrl+click \(go to Declaration, brief info, tool tip\) Ctrl+N \(go to class\) Ctrl+Shift+N \(go to file\) Ctrl+Alt+Shift+N \(go to symbol\) Ctrl + F12 \(method list popup in class\)
* editor, tool window ESC \(back to editor\) F12 \(last used tool\) Shift+ESC \(hide tool and go to editor\) Alt+ESC \(close tool and go to editor\) shift + ctr + F12: \(close all tool, only editor\)

Multicoursor: Alt + Click Find usage: Alt + F7 Jump to syntac error: F2, shift + F2 View inheritance hierarchy: Ctrl + H Code completion: Ctrl + space Complete current statement\(if, try,…\): Ctrl + shift + enter Rename: shift + F6 Column mode: Alt + shift + insert Show option for error: Alt + enter ex. RegExp: regular expression editor Double click\(select\): Ctrl + w \*\*?? ?? Code format: Ctrl + alt + L Code bookmark ctrl + F11: set F11: set shift + F11: view all Select text, word, line text: ctrl + shift &lt;-, ctrl + shift + -&gt; line: home / end\(cursor move\), shift + home/end\(select\) Focus to the editor back: Esc Last used tool: F12 Hide tool: shift + Esc Close tool: alt + Esc Open brief info\(tool tip\): ctrl + click Go def? ?? ??: ctrl + click = ctrl + B Open quick definition window: ctrl + shift + i Open view doc window: ctrl + Q Tab, reverseTab: shift + Tab

