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


**Git的提交id （commit id）是一个摘要值，这个摘要值实际上是个sha1计算出来的**

对于user.name与user.email来说，有3个地方可以设置
1. /etc/gitconfig（针对整个操作系统的,几乎不会使用） `git config --system`  此文件有可能不存在需要自己创建
2. ~/.gitconfig（很常用, 针对特定用户）            `git config --global`
3. 当前项目的 .git/config文件中                   `git config --local`

以上优先级越具体越高, 也就是说3>2>1, 同时配置的情况下取最高优先级的.

具体参数和用法可以直接执行 `git config`

```shell
-- set a property of the configuration
git config user.name 'a new name'
```

```shell
-- remove a property from the configuration
git config --local --unset user,name
```


Note: all above usage can be found from executing alone command **`git config`**

```shell
GitTutorial ➤ git config                                                                                                                                                      git:main*
usage: git config [<options>]

Config file location
    --global              use global config file
    --system              use system config file
    --local               use repository config file
    --worktree            use per-worktree config file
    -f, --file <file>     use given config file
    --blob <blob-id>      read config from given blob object

Action
    --get                 get value: name [value-pattern]
    --get-all             get all values: key [value-pattern]
    --get-regexp          get values for regexp: name-regex [value-pattern]
    --get-urlmatch        get value specific for the URL: section[.var] URL
    --replace-all         replace all matching variables: name value [value-pattern]
    --add                 add a new variable: name value
    --unset               remove a variable: name [value-pattern]
    --unset-all           remove all matches: name [value-pattern]
    --rename-section      rename section: old-name new-name
    --remove-section      remove a section: name
    -l, --list            list all
    --fixed-value         use string equality when comparing values to 'value-pattern'
    -e, --edit            open an editor
    --get-color           find the color configured: slot [default]
    --get-colorbool       find the color setting: slot [stdout-is-tty]

Type
    -t, --type <type>     value is given this type
    --bool                value is "true" or "false"
    --int                 value is decimal number
    --bool-or-int         value is --bool or --int
    --bool-or-str         value is --bool or string
    --path                value is a path (file or directory name)
    --expiry-date         value is an expiry date

Other
    -z, --null            terminate values with NUL byte
    --name-only           show variable names only
    --includes            respect include directives on lookup
    --show-origin         show origin of config (file, standard input, blob, command line)
    --show-scope          show scope of config (worktree, local, global, system, command)
    --default <value>     with --get, use default value when missing entry
```

Demo of command: 
```shell 
git reset HEAD src/mygit/a.txt 
```
Snip:
![Xnip2024-04-04_18-49-42.png](pics%2FXnip2024-04-04_18-49-42.png)

![Xnip2024-04-05_08-03-16.png](pics%2FXnip2024-04-05_08-03-16.png)
![Xnip2024-04-05_08-13-01.png](pics%2FXnip2024-04-05_08-13-01.png)
截止此时, test1.txt 和test2.txt 都在版本库了. 如果此时想将版本库里的文件删掉
![Xnip2024-04-05_08-28-46.png](pics%2FXnip2024-04-05_08-28-46.png)
![Xnip2024-04-05_08-41-02.png](pics%2FXnip2024-04-05_08-41-02.png)

结合上面的所有可以看出, git rm 删除是首先将文件从版本库移到暂存区, git reset HEAD 再将暂存区移到已修改. 最后 git checkout 是恢复到上一次提交. 也就是说最后回退恢复了.<br/>
如果不恢复, git rm 后就是要将文件删除掉, 该怎么办? 下图给你答案:
![Xnip2024-04-05_09-07-32.png](pics%2FXnip2024-04-05_09-07-32.png)

直接用系统命令rm删除文件:
![Xnip2024-04-05_09-16-16.png](pics%2FXnip2024-04-05_09-16-16.png)
![Xnip2024-04-05_09-23-21.png](pics%2FXnip2024-04-05_09-23-21.png)
可以看出rm 和 git rm都可以执行删除操作, 最终结果也一样,但是中间状态是不一样的.

**git rm：**
1. 删除了一个文件
2. 将被删除的文件纳入到暂存区（stage，index）
若想恢复被删除的文件，需要进行两个动作：
a. git reset HEAD testZ。txt，将待删除的文件从暂存区恢复到工作区 
b. git checkout -- test2.txt 将工作区中的修改丟弃掉



如何修改commit message:
```shell
git commit --amend -m 'modified commit message'
```

```shell

```


git log 美化:
```shell
git log --pretty=format:"%h - %an, %ar : %S"
```
```shell
git log --pretty=oneline
```
```shell
git reflog
```
-p 展开显示每次提交的内容差异
-n 仅显示最近的n次更新
-stat 仅显示简要的增改行数统计



Git配置

下面三行代码任意一行都可以获取帮助
```shell
git help config
git config - - help
man git-config
```


# Episode 6: .gitignore 相关

# Episode 7: 分支的重要操作






































**Untracked:** Files that are not tracked by Git.
> 1. Transition to Unmodified: Occurs after adding the file with git add and committing it with git commit.
> 2. Transition to Modified: Occurs after modifying an untracked file.<br>

**Unmodified:** Files that have been committed and their contents have not been changed.
> 1. Transition to Modified: Occurs after modifying the file with git checkout or git reset HEAD.
> 2. Transition to Deleted: Occurs after removing the file with git rm.

**Modified:** Files that have been modified since the last commit.
> 1. Transition to Staged: Occurs after adding the file with git add and committing it with git commit.
> 2. Transition to Unmodified: Occurs after resetting the file with git reset HEAD.

**Staged:** Files that have been added to the staging area but not yet committed.
> 1. Transition to Modified: Occurs after resetting the file with git reset HEAD.
> 2. Transition to Unmodified: Occurs after committing the file with git commit.
> 3. Transition to Untracked: Occurs after removing the file with git rm.

**Deleted**: Files that have been deleted from the working directory.
> 1. Transition to Untracked: Occurs after committing the deletion with git commit.






