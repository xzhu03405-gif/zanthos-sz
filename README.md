# zanthos-sz

ZANTHOS 运营站「固定入口」跳转页（GitHub Pages）。

- `index.html` —— 固定网址 `https://<user>.github.io/zanthos-sz/`，访问时自动跳转到当前 Cloudflare 快速隧道网址。
- `current-url.json` —— 由深圳节点 `free-redirect` 自动化脚本在隧道网址变化时**自动更新并推送**，请勿手动长期修改（临时改一下会被下一轮覆盖）。

## 自动更新链路
深圳节点 `free-redirect-detect` 计划任务（每 5 分钟）：
1. `detect-tunnel-url.py` 读 cloudflared 日志，提取当前隧道网址；
2. 网址变化 → 写 `changed.flag`；
3. `update-redirect.py` 把新网址写入本仓库 `current-url.json` 并 `git push`（经部署私钥 `github-zanthos`）；
4. GitHub Pages 约 1 分钟内生效，访客下次打开固定网址即跳到新隧道。

## 本地维护
```bat
cd D:\free-redirect\pages
git pull
git add current-url.json
git commit -m "manual update"
git push
```
