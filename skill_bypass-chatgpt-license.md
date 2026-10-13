---
name: bypass-chatgpt-license
description: 绕过 ChatGPT 桌面应用的 Microsoft Store 许可证验证
---

# ChatGPT 许可证绕过技能

自动化修改和重新打包 ChatGPT 桌面应用，绕过 Microsoft Store 许可证验证。

## 使用方法

```
/bypass-chatgpt-license
```

或在更新时提供 MSIX 文件路径：
```
/bypass-chatgpt-license --msix D:\path\to\ChatGPT.msix
```

## 工作流程

1. **创建自签名证书**（首次运行）
   - 创建代码签名证书
   - 导出 PFX 和 CER 文件
   - 安装到受信任的根证书颁发机构

2. **导出或解包 MSIX**
   - 从已安装应用导出文件
   - 或解包提供的 MSIX 文件

3. **修改 AppxManifest.xml**
   - 移除 `appLicensing` capability
   - 修改 Publisher 为自签名证书

4. **重新打包**
   - 使用 makeappx.exe 打包

5. **签名**
   - 使用 signtool.exe 和自签名证书签名

6. **安装**
   - 卸载旧版本
   - 安装修改后的版本
   - 启动应用

## 技术原理

Microsoft Store 应用通过 `appLicensing` capability 调用 ClipSVC 服务验证许可证。移除此 capability 后，应用不再尝试验证许可证。

## 文件位置

- **工作目录**: `D:\OpenAI\MSIX_Workspace\`
- **证书**: `D:\OpenAI\MSIX_Workspace\ChatGPT_SelfSign.*`
- **文档**: `D:\OpenAI\reverse_engineering_notes\`
- **脚本**: `D:\OpenAI\bypass_chatgpt_license.ps1`

## 更新流程

当 OpenAI 发布新版本：
1. 下载或安装新版本
2. 运行此技能
3. 自动应用相同的修改
4. 安装修改后的版本

## 前置要求

- Windows 10/11
- 开发者模式已启用
- Windows SDK（包含 makeappx 和 signtool）
- 管理员权限（首次安装证书）

## 注意事项

- 证书有效期 5 年
- 每次更新使用同一证书
- 代理配置：http://127.0.0.1:7897
