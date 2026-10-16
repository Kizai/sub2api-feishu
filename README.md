# sub2api-feishu

Sub2API 上游版本 + 飞书告警 webhook 补丁的自动构建流水线。

上游官方不内置 webhook 推送，此补丁（patches/feishu-alert-webhook.patch）为运维告警增加飞书群推送：
- OpsEmailNotificationConfig 增加 feishu 段（enabled / webhook_url / min_severity）
- 告警触发 + 恢复都推送，1s 节流

## 升级新版本
1. 改 UPSTREAM_TAG 文件为新 tag（如 v0.2.18）
2. commit + push → Actions 自动构建并发布 Release（tag: <版本>-feishu.1）
3. 服务器执行 /root/scripts/sub2api_upgrade_ci.sh 拉取部署

若补丁对新版本冲突，先在本仓库更新 patches/ 再推。
