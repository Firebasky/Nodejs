# javascript大小写特性

在javascript中有几个特殊的字符需要记录一下

对于`toUpperCase()`:

```
字符"ı"、"ſ" 经过toUpperCase处理后结果为 "I"、"S"
```

对于`toLowerCase()`:

```
字符"K"经过toLowerCase处理后结果为"k"(这个K不是K)
```

在绕一些规则的时候就可以利用这几个特殊字符进行绕过

## **CTF题实例 - Hacktm中的一道Nodejs题**

题目部分源码：

```js
function isValidUser(u) {
  return (
    u.username.length >= 3 &&
    u.username.toUpperCase() !== config.adminUsername.toUpperCase()
  );
}

function isAdmin(u) {
  return u.username.toLowerCase() == config.adminUsername.toLowerCase();
}
```

解题时需要登录管理员的用户名，但是在登录时，`isValidUser`函数会对用户输入的用户名进行`toUpperCase`处理，再与管理员用户名进行对比。如果输入的用户名与管理员用户名相同，就不允许登录。

但是我们可以看到，在之后的一个判断用户是否为管理员的函数中，对用户名进行处理的是`toLowerCase`。所以这两个差异，就可以使用大小写特性来进行绕过。

题目中默认的管理员用户名为：hacktm

所以，我们指定登录时的用户名为：hacKtm 即可绕过`isValidUser`和`isAdmin`的验证。

题目完整Writeup:[HackTM中一道Node.js题分析(Draw with us)](https://xz.aliyun.com/t/7177)

## MMCTF

`nodejs`

```js
router.post('/admin', function (req, res, next){
  if(req.body.name === undefined)
  {
    res.send("what's your name?");
  }
  else{
    let name=req.body.name.toString();
    if(name.toLowerCase()!=="admin"&&name.toUpperCase()==="ADMIN")
    {
      req.session.man.attack=300;
      res.send("you've been stronger")
    }
    else{
      res.send("you are not admin!!");
    }
  }
});
```

`exp.js`

```js
for(var i=300;i<=305;i++){//65535
    console.log(String.fromCharCode(i)+i);
    var name="admin";
    name='adm'+String.fromCharCode(i)+'n';
    console.log(name);
    if(name.toLowerCase()!=="admin"&&name.toUpperCase()==="ADMIN")
    {
        alert('success'+':'+String.fromCharCode(i)+':'+i);
        console.log('success');
    }
    else{
        console.log('fail');
    }   
}
```

