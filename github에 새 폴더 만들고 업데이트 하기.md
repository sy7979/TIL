### github에 새 폴더 만들고 업데이트 하기

홈페이지에서 새 폴더 만들고, 

```
git remote add origin https://github.com/username/python.git
```
웹에서 이 정보 복사

```
student@DESKTOP MINGW64 ~/python
$ git init

student@DESKTOP MINGW64 ~/python (master)
$ git add .

student@DESKTOP MINGW64 ~/python (master)
$ git commit -m "add file"

student@DESKTOP MINGW64 ~/python (master)
$ git remote add origin https://github.com/usename/python.git

student@DESKTOP MINGW64 ~/python (master)
$ git push origin master


```

```
student@DESKTOP MINGW64 ~/TIL (master)
$ git add .

student@DESKTOP MINGW64 ~/TIL (master)
$ git commit -m 'addfile'


student@DESKTOP MINGW64 ~/TIL (master)
$ git push origin master

```





폴더 삭제하기

```
student@DESKTOP MINGW64 ~/homeworkshop (master)
$ rm -rf .git

student@DESKTOP MINGW64 ~/homeworkshop
$ git init

student@DESKTOP MINGW64 ~/homeworkshop (master)
$ git add .

student@DESKTOP MINGW64 ~/homeworkshop (master)
$ git commit -m "add file"

student@DESKTOP MINGW64 ~/homeworkshop (master)

```

