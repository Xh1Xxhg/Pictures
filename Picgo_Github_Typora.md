# Picgo_Github_Typora

# Github

新建仓库，设置仓库名、描述等

# Picgo

```bash
npm install picgo -g
picgo install github-plus
```

# Typora

- 文件->偏好设置->图像->上传服务设定

![image-20240530001052308](https://cdn.jsdelivr.net/gh/Xh1Xxhg/Pictures@main/CTF/image-20240530001052308.png)

- 打开配置文件

```json
{
  "picBed": {
    "uploader": "githubPlus",
    "current": "githubPlus",
    "githubPlus": {
      "branch": "main",
      "origin": "github",
      "repo": "Xh1Xxhg/Pictures",
       // 固定前缀https://cdn.jsdelivr.net/gh/
       // 用户名/仓库名/分支 Xh1Xxhg/Pictures@main
      "customUrl": "https://cdn.jsdelivr.net/gh/Xh1Xxhg/Pictures@main",
      "path": "CTF",
       // token，记得开放repo权限
      "token": ""
    }
  },
  "picgoPlugins": {
    "picgo-plugin-github-plus": true,
    "picgo-plugin-gitee-uploader": true
  },
  "picgo-plugin-github-plus": {
    "lastSync": "2024-05-29 11:55:17"
  }
}
```

- 测试是否成功配置

![image-20240530002249111](https://cdn.jsdelivr.net/gh/Xh1Xxhg/Pictures@main/CTF/image-20240530002249111.png)