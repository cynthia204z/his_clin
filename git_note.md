# GIT

基礎用法

```bash
git add . 
> 'add所有異動檔案'

git commit -m '20220315更新'
> '更新訊息'

git push
> '將commit的版本推到遠端'

git status
> '查看狀態'
```



[Git 取消未push的commit](https://matthung0807.blogspot.com/2021/07/git-cancel-last-unpushed-local-commit.html)

> 捨棄前次commit，回復上一動

```bash
git reset HEAD^
> '取消前次commit(不保留add狀態)'

git reset --soft HEAD^
> '取消前次commit(保留add狀態)'

git reset HEAD~2
> '取消多次commit(範例2次)'
```







https://tso1158687.github.io/blog/2020/02/12/remove-nodemodules/

















# 標題1

## 標題2

### 標題3

#### 標題4

##### 標題5

###### 標題6

```js
let myNum = 1;
console.log(myNum);
function getCount(num1, num2) {
  return (num1 + myNum) / num2
}
let herNum = 5;
getCount(2, 5);
```

