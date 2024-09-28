# git action笔记

- git action每一个job都是一个docker容器，因此跨job的文件需要通过artifact上传和下载，跨job的参数需要$GITHUB_OUTPUT来
- 注意注释的部分缩进要退到run里面，否则报错not valid
我不知道为什么，在本地建立yml时gitaction的流程名字不是yml设置的
- 在 Bash 中，要为变量赋值， =号周围不应有空格
- 多搜索别人的插件使用
## 开头
```yaml
on:
  push:
  workflow_dispatch: # 允许手动在action页面触发
  # schedule:
    # - cron: '*/30 * * * *' # 每30分钟检查一次
```
注意，dev分支的workflow操作不被认可，如果要测试现在暂时新建一个workflow在main里面来调整

## 参数设定与调用
1. jobs内，可以跨steps。用ENV

注意，创建或更新环境变量的步骤无权访问新值，但作业中的所有后续步骤都可以访问

在 Bash 中，${CHROME_PLUS_TAG} 和 $CHROME_PLUS_TAG 都可以用来引用变量，功能相同。但使用 ${} 更加清晰，尤其是在变量名后面紧跟着字符时，可以避免解析错误。

```yaml
# 情况1，输出“111+222”
run: |
    new_version = 222
    echo "NEW_VERSION=${new_version}" >> $GITHUB_ENV
    echo "${NEW_VERSION}+111" 
# 情况2，输出“ttt+222”
run: |
    echo "NEW_VERSION=ttt" >> $GITHUB_ENV
    echo "${NEW_VERSION}+222" 
```
2. 跨jobs。用OUTPUTS
```yaml
jobs:
    job1:
    outputs: # 设定要传出的outputs
      should_run: ${{ steps.compare_versions.outputs.should_run }}
    steps:
        - name: CC
            id: compare_versions
            run: |
                echo "should_run=1" >> $GITHUB_OUTPUT
    job2:
    needs: check
    # 跨jobs变量借用needs的前置job
    if: ${{ needs.check.outputs.should_run == 1 }}
    steps: ...
```

## if else
```yaml
if [ "$OLD_VERSION" != "$NEW_VERSION" ] || [ "${{ github.event_name }}" == 'workflow_dispatch' ]; then
    echo "Versions are different"
    echo "should_run=1" >> $GITHUB_OUTPUT
else
    echo "Versions are the same"
    echo "should_run=0" >> $GITHUB_OUTPUT
fi
```