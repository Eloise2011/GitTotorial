```shell
-- Initializing git repository in current working directory
git init
```

```shell
-- Adding the modified files into the staging area, only those files already in the staging area can be further committed and pushed into the version repository
git add 
```

```shell
-- checking the status of each file under the repository
git status
```

result of git status like below:
![Xnip2024-04-04_17-18-42.png](pics%2FXnip2024-04-04_17-18-42.png)

The prompt of 1st part, namely the Changes to be committed, saying: "(use "**git rm --cached ‹file›**... to unstage)"
So, literally, it means that we can unstage the changes that we added into the staging area.

```shell
-- reverting the file from staging area to modified, i.e. untracked files
git rm --cached pics/Xnip2024-04-04_17-18-42.png
```
注意: 文件路径要正确, 否则会报错.
执行完之后, 文件颜色从绿变红,也可以看出已经退回到已修改状态.