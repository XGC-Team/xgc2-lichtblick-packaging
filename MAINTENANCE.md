# Lichtblick 维护边界

本文档是 XGC2 集成 Lichtblick 的强制维护规约。目标是确保 APT 只发布我们实际维护和
使用的 Lichtblick 源码，同时保持源码、打包、CI 和签名仓库职责分离。

## 唯一发布链

- `lxk36/xgc2-lichtblick` 的 `xgc2` 分支是唯一允许的产品源码输入；
- `xgc2-lichtblick-packaging` 是唯一 Lichtblick Debian 打包与发布入口；
- `lichtblick.lock` 必须同时固定维护仓库、`xgc2` 分支和精确 commit SHA；
- `xgc2-devops` 只登记 packaging 产品，源码仓不得重复声明同名产品；
- APT 签名和索引发布仍由中央发布器执行。

禁止直接从 `lichtblick-suite/lichtblick` 的 tag、其他 fork、工作区未提交内容或临时
构建目录生成正式包。

## Packaging 可以负责什么

- 校验维护分支和不可变 SHA；
- 固定 Node、Yarn、FPM 等构建输入；
- 从同一源码构建 `xgc2-lichtblick-web` 和可选的 `xgc2-lichtblick` 桌面包；
- 执行六个平台组合的安装、启动和卸载验证；
- 维护包元数据、CI、发布和源码锁新鲜度检查。

Packaging 不得在构建时偷偷注入未提交补丁，也不得从其他产品仓库拼装 Lichtblick
制品。

## 升级检查

维护分支前进后必须：

1. 审阅 `xgc2` 分支的新 commit，并确认其为实际使用的源码；
2. 更新 `lichtblick.lock` 的精确 SHA；
3. 在 `.xgc2/product.yml` 增加 Debian revision 和全部发行版版本；
4. 运行 packaging 合规检查、Web 测试和 GitHub CI 六平台包验证；
5. 仅在上述检查通过后，通过中央发布器更新 Lichtblick 的 APT 坐标；
6. 审计 APT 索引、签名及六个平台的新版本，不顺带发布其他产品。
