# Flutter 问题记录

## 解决 `iproxy` cannot be opened because the developer cannot be verified 问题(参考)[https://medium.com/codespace69/flutter-iproxy-cannot-be-opened-because-the-developer-cannot-be-verified-d1ad3cb9ebd9]

```bash
sudo xattr -d com.apple.quarantine /User/jinping/software/flutter/bin/cache/artifacts/usbmuxd/iproxy
```

---

## flutter-qiniu 下载慢的问题

```bash
# 1.
cd ~/.cocoapods/repos

# 2. <name> 是trunk或master
pod repo remove <name> 

# 3.
git clone https://mirrors.tuna.tsinghua.edu.cn/git/CocoaPods/Specs.git master
```

---

## Mac ShadowSocks Proxy in terminal

```zsh
# 1.
vim ~/.zshrc

# 2. 添加下列内容

`````````
# proxy list
>alias proxy='export all_proxy=socks5://127.0.0.1:1086'

>alias unproxy='unset all_proxy'
`````````

# 3. 保存退出

# 4.
source ~/.zshrc

```

> 使用方法：先 运行`proxy`, 然后用`curl cip.cc`检查是否代理成功；取消代理：运行`unproxy`

---
