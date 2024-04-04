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
1. /etc/gitconfig（针对整个操作系统的,几乎不会使用） `git config --system`
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