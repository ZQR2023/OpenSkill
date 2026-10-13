# ChatGPT 许可证绕过 Skill
主要针对Win 10的部分版本，使用改skill 搭配claudecode
绕过 ChatGPT 桌面应用的 Microsoft Store 许可证验证。


## 使用方法

需要从gpt官网下载 exe 安装包，然后搭配claude+skill  完成安装，
缺点是 成功安装后的gpt 无法进行自动更新
```

## 工作流程

1. 创建自签名证书（首次运行）
2. 导出或解包 MSIX 应用
3. 修改 AppxManifest.xml，移除许可证验证
4. 重新打包并签名
5. 安装修改后的版本

## 前置要求

- Windows 10/11
- 开发者模式已启用
- Windows SDK（makeappx 和 signtool）
- 管理员权限（首次运行）

## 注意事项

- 证书有效期 5 年
- 每次更新使用同一证书
- 仅供学习研究使用

