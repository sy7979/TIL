### gitlab에 등록하는방법



1. 초기 설정

```python
student@DESKTOP MINGW64 ~/homeworkshop (master)
$ cd ..

student@DESKTOP MINGW64 ~
$ cd project/

student@DESKTOP MINGW64 ~/project
$ cd pjt01/

student@DESKTOP MINGW64 ~/project/pjt01 (master)
$ git remote -v
origin  https://github.com/sy7979/project01.git (fetch)
origin  https://github.com/sy7979/project01.git (push)

student@DESKTOP MINGW64 ~/project/pjt01 (master)
$ git remote add gitlab https:~~~~~

student@DESKTOP MINGW64 ~/project/pjt01 (master)
$ git push gitlab master


```


2. 그 다음부터..
```python
git add .

git commit -m'add file'

git push gitlab master
```

