# SemVer (Semantic Versioning) 语义化版本规范

<a name="GieDt"></a>
# 版本错误引发的构建bug
起因是项目要兼容IE浏览器，需要将代码从ES6转义成ES5。在最新一次构建过程中，发现有部分代码 `cosnt` 没有被编译成 `var` 。<br />![image.png](https://cdn.nlark.com/yuque/0/2020/png/1537754/1605072844287-f43a0403-91fe-46c9-b334-d7cf5a458280.png#align=left&display=inline&height=827&margin=%5Bobject%20Object%5D&name=image.png&originHeight=827&originWidth=455&size=47080&status=done&style=none&width=455)<br />最终定位到了出错代码是  `asn1.js` ，但是比较奇怪的是只有这个包的代码没有转义。看了一下这包的更新记录，早在三年前更新了就已经更新成了ES6的语法，<br />![image.png](https://cdn.nlark.com/yuque/0/2020/png/1537754/1605072894967-c0bce189-aca3-490d-80a1-de7237b435ee.png#align=left&display=inline&height=124&margin=%5Bobject%20Object%5D&name=image.png&originHeight=124&originWidth=1297&size=12315&status=done&style=none&width=1297)<br />并且我在 `package.json` 中指定 `asn1.js` 版本，但最终 `node_modules` 下载的还是最新版本的代码，那么问题就不是出在这个包，可能是其他引用这个包造成的问题，所以按图索骥找到了 `parse-asn1` 这个包，这个包的更新记录显示三个月前 `asn1.js` 版本号发生了变化，<br />![image.png](https://cdn.nlark.com/yuque/0/2020/png/1537754/1605073024563-2a55a698-9df9-44da-9ea9-e8133999b51b.png#align=left&display=inline&height=436&margin=%5Bobject%20Object%5D&name=image.png&originHeight=436&originWidth=1638&size=46159&status=done&style=none&width=1638)<br />并且在 [Issues](https://github.com/crypto-browserify/parse-asn1/issues/41) 里很多人使用新版本导致构建出现了问题。<br />![image.png](https://cdn.nlark.com/yuque/0/2020/png/1537754/1605073199695-71a5fab3-c4f7-4d77-9477-0c7f827a2716.png#align=left&display=inline&height=921&margin=%5Bobject%20Object%5D&name=image.png&originHeight=921&originWidth=1362&size=118499&status=done&style=none&width=1362)<br />基本可以确定是由于 `parse-asn1` 使用了新版本，导致出错。
<a name="Jmx0a"></a>
# 依赖地狱
当安装某个包是，发现这个有引用了其他的包，如果安装包之间依赖过高可能会面临版本依赖被锁死或版本混乱变得不够简便和可靠那么此时你就陷入了"依赖地狱"之中。<br />为了避免这种情况，github创始人TomPreston-Werner起草了[Semantic Versioning(语义化版本表示)](https://semver.org/) 作为指导规范
<a name="hlIir"></a>
# 版本格式
 版本格式： 主版本号.次版本号.修订号。规则如下:

1. 主版本号：当你做了不兼容的API修改
1. 次版本号：当你做了向下兼容的功能性新增
1. 修订号：当你做了向下兼容的问题修正

先行版本号及版本编译元数据可以加到“主版本号.次版本号.修订号”的后面，作为延伸。
<a name="ycwta"></a>
# 版本
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1537754/1605077547142-443ba9df-612c-4f12-807e-0183fe000d9c.png#align=left&display=inline&height=939&margin=%5Bobject%20Object%5D&name=image.png&originHeight=939&originWidth=298&size=34794&status=done&style=none&width=298)（vue版本更新日志,2020.11.11）<br />版本可以分为：

1. alpha：内部测试版本
1. beta：公开测试版本
1. rc：Release Candidate，最终测试版本
1. X.Y.Z： 正式版本
<a name="1ZnGd"></a>
# 版本号命名规范

1. 版本号必须是 `X.Y.Z` 的非负整数格式。每个元素必须以数值来递增。例如： 1.9.1 -> 1.10.0 -> 1.11.0
1. 版本发布后，禁止改变该版本内容，任何修改必须以新版发行
1. 主版本号为零（0.Y.Z）的软件处于开发初始阶段，一切可能随时改变，这样的公共API必应视为稳定版本
1. 1.0.0 的版本用于界定公共API的形成。
1. 次版本号递增时，修订号必须归零；主版本号递增时，次版本号、修订号必须归零
1. 版本的优先层级：主版本号>次版本号>修订号>rc.大数>rc.小数>beat.大数>beat.小数>alpha.大数>alpha.小数
<a name="EJ1vv"></a>
# npm包依赖
```javascript
"dependencies": {
	"vue": "^2.6.10",
}
```
```javascript
"dependencies": {
	"vue": "~2.6.10",
}
```
`^` ： 代表会匹配更新次版本号，但不包括主版本号<br />`~` ：代表会匹配更新修订号，但不包括次版本号<br />

