# my-local-record

## Project setup
```
pnpm install
```

### Compiles and hot-reloads for development
```
pnpm run serve
```

### Compiles and minifies for production
```
pnpm run build
```

### Lints and fixes files
```
pnpm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

## 可以优化的地方
1. 从localStorage读取
2. 存入localStorage
3. 排序
4. 修改顺序
3. 增加字
4. 字带词和造句
5. 字带拼音
6. 字带声音

## 部署步骤
1. npm run build
2. git checkout --orphan gh-pages
3. git rm -rf .
4. cp -r dist/* .  # 你的 build 输出目录
5. git add . & git commit -m "Deploy to gh-pages" & git push origin gh-pages --force
6. 去 GitHub 仓库 Settings → Pages：Source 选择 gh-pages 分支

