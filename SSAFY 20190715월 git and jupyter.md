### SSAFY Python 20190715월



1. ##### git.bash에서 내가 올린 파일 복사해오기

```

student@DESKTOP MINGW64 ~
$ git clone https://github.com/sy7979/TIL.git
fatal: destination path 'TIL' already exists and is not an empty directory.

student@DESKTOP MINGW64 ~
$ git clone https://github.com/sy7979/TIL.git

```


2. ##### why python?

   왜 파이썬을 사용하는가??

- easy : 영어 문장을 직독직해 하는 느낌으로 사용 가능
- strong : pypi.org : python에서 install,import 할 수 있는 모듈(함수)들이 굉장히 많고, 쉽게 가져다 쓸 수 있다.
  ex) BeautifulSoup, tensorflow, -----
- Fast : 사용하기 쉽고, 빠르다.



3. ##### Consol , vscode, ID(통합계발문서, 예)pycharm), **jupyter**(코드를 셀 단위로실행, 블록만큼만 실행 하고 그 결과를 활용할 수 있다.)-----------

   **jupyter**: python 실행창과 markdown 문서 작성을 동시에 할 수 있음
   
   <jupyter 설치 방법>

```
student@DESKTOP MINGW64 ~
$ pip install jupyter
```

```
student@DESKTOP MINGW64 ~
$ jupyter notebook
```

​		run ==> crome창이 자동으로 popup



​		<내가 만든 폴더 안에 jupyter notebook실행>

```
student@DESKTOP MINGW64 ~
$ mkdir python

student@DESKTOP MINGW64 ~
$ cd python

student@DESKTOP MINGW64 ~/python
$ jupyter notebook
```

나의 pc상의 python 폴더와 jupyter notebook이 서로 연동된다.

그렇기 때문에 쥬피터를 사용할 때 git bash 에서 jupyer notebook이 실행되고 있어야 한다.

​	< 앞으로 jupyter notebook 실행시키려면>

```
student@DESKTOP MINGW64 ~
$ cd python

student@DESKTOP MINGW64 ~/python
$ jupyter notebook
```





4. ##### jupyter 사용법

   - 마크다운, 코드

   - line 순서에 상관없이 실행 가능, 내가 실행(ctrl+enter 등등 으로..)하는 순서대로 실행된다.

   - git bash 에서 jupyer notebook이 실행되고 있어야 jupyter 에서도 실행이 가능하다.

   - ctrl + enter : 현재 위치에서 실행

     alt + enter :  새로운 셀 생성 (새로운 셀 삽입)

     shift + enter : 아래쪽으로 내려가면서 실행

   - esc : 초록 --> 파랑 : 셀 이동 가능하게 됨

     enter : 파랑 --> 초록 : input mode, 작성 가능하게 된다.

   - ln[] : []안에 내가 실행시킨 순서가 뜬다. code의 순서는 줄의 순서가 아닌 []안의 순서대로 진행된다.

   - 변수는 누적되어서 저장 된다.

     1. x = 1
     2. x = 1, 2, 3

     이면, x = 1, 2, 3으로 저장된다. 원하는 변수 값을 가장 **마지막**에 실행하여야 한다.

     

     ** jupyter  theme 바꾸기

     ```
     student@DESKTOP MINGW64 ~/python
     
     $ pip intall jupyterthemes
     
     $ jt -l
     
     $ jt t oceans16
     
     ```

     

     