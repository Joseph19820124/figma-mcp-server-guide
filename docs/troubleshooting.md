# Troubleshooting Guide | 故障排除指南

This guide provides solutions to common issues when setting up and using Figma MCP Server.

本指南提供设置和使用Figma MCP服务器时常见问题的解决方案。

---

## Quick Diagnostics | 快速诊断

### Step 1: Check Server Status | 步骤1: 检查服务器状态

**English**: Verify that the Figma MCP server is running:
1. Open Figma Desktop app
2. Go to **Help and Account** > **Preferences**
3. Look for **Dev Mode** section
4. Ensure **Enable Dev Mode MCP Server** is toggled ON
5. You should see: "Server running at http://127.0.0.1:3845/sse"

**中文**: 验证Figma MCP服务器正在运行：
1. 打开Figma桌面应用
2. 转到 **帮助和账户** > **首选项**
3. 查找 **开发模式** 部分
4. 确保 **启用开发模式MCP服务器** 已打开
5. 您应该看到："服务器运行在 http://127.0.0.1:3845/sse"

### Step 2: Test Connection | 步骤2: 测试连接

**English**: Test if the server is accessible:
```bash
curl http://127.0.0.1:3845/sse
```
Expected: Server should respond (not refuse connection)

**中文**: 测试服务器是否可访问：
```bash
curl http://127.0.0.1:3845/sse
```
预期：服务器应该响应（不是拒绝连接）

---

## Common Issues | 常见问题

### Issue 1: MCP Server Not Found | 问题1: 找不到MCP服务器

#### Symptoms | 症状
- IDE shows "No MCP servers found"
- Connection timeout errors
- 显示"未找到MCP服务器"
- 连接超时错误

#### Solutions | 解决方案

**English**:
1. **Restart Figma Desktop**: Close and reopen the app
2. **Check Port Availability**: Ensure no other service uses port 3845
3. **Firewall Settings**: Allow Figma through your firewall
4. **Antivirus**: Temporarily disable to test if it's blocking the connection

**中文**:
1. **重启Figma桌面应用**: 关闭并重新打开应用
2. **检查端口可用性**: 确保没有其他服务使用端口3845
3. **防火墙设置**: 允许Figma通过防火墙
4. **杀毒软件**: 临时禁用以测试是否阻止连接

### Issue 2: Authentication Errors | 问题2: 身份验证错误

#### Symptoms | 症状
- "Invalid API token" messages
- 403 Forbidden errors
- "无效API令牌"消息
- 403禁止访问错误

#### Solutions | 解决方案

**English**:
1. **Regenerate Token**: Create a new Figma API token
2. **Check Permissions**: Ensure token has "File content" and "Dev resources" read access
3. **Token Format**: Verify token is correctly copied (no extra spaces)
4. **Expiration**: Check if token has expired

**中文**:
1. **重新生成令牌**: 创建新的Figma API令牌
2. **检查权限**: 确保令牌具有"文件内容"和"开发资源"读取权限
3. **令牌格式**: 验证令牌正确复制（无多余空格）
4. **过期时间**: 检查令牌是否已过期

### Issue 3: IDE Configuration Problems | 问题3: IDE配置问题

#### For Cursor | 对于Cursor

**Symptoms | 症状**:
- MCP server not appearing in agent mode
- Configuration not saving
- 代理模式中未显示MCP服务器
- 配置未保存

**Solutions | 解决方案**:

**English**:
1. **Check Settings Path**: Ensure you're editing global settings, not workspace
2. **JSON Syntax**: Validate JSON syntax using online validator
3. **Restart Required**: Close and reopen Cursor after configuration changes
4. **Agent Mode**: Make sure agent mode is enabled in chat

**中文**:
1. **检查设置路径**: 确保编辑全局设置，而非工作区设置
2. **JSON语法**: 使用在线验证器验证JSON语法
3. **需要重启**: 配置更改后关闭并重新打开Cursor
4. **代理模式**: 确保在聊天中启用代理模式

#### For VS Code | 对于VS Code

**Symptoms | 症状**:
- MCP not working with Copilot
- Settings not recognized
- MCP无法与Copilot配合使用
- 设置未被识别

**Solutions | 解决方案**:

**English**:
1. **GitHub Copilot**: Ensure Copilot extension is installed and active
2. **Settings Location**: Edit User settings.json, not workspace
3. **Reload Window**: Use Cmd/Ctrl+Shift+P > "Developer: Reload Window"
4. **Extension Conflicts**: Disable other AI extensions temporarily

**中文**:
1. **GitHub Copilot**: 确保安装并激活Copilot扩展
2. **设置位置**: 编辑用户settings.json，而非工作区
3. **重新加载窗口**: 使用Cmd/Ctrl+Shift+P > "Developer: Reload Window"
4. **扩展冲突**: 临时禁用其他AI扩展

### Issue 4: Design Reading Problems | 问题4: 设计读取问题

#### Symptoms | 症状
- "Cannot read design" errors
- Empty responses from MCP
- "无法读取设计"错误
- MCP返回空响应

#### Solutions | 解决方案

**English**:
1. **Component Issues**: Try detaching component instances
2. **Frame vs Group**: Convert groups to frames
3. **File Permissions**: Ensure you have view access to the Figma file
4. **File Size**: Very large files may cause timeouts
5. **Design Complexity**: Simplify complex nested structures

**中文**:
1. **组件问题**: 尝试分离组件实例
2. **框架与组**: 将组转换为框架
3. **文件权限**: 确保您有Figma文件的查看权限
4. **文件大小**: 非常大的文件可能导致超时
5. **设计复杂性**: 简化复杂的嵌套结构

---

## Performance Issues | 性能问题

### Slow Response Times | 响应时间慢

**English**:
1. **Close Unused Files**: Limit open Figma files
2. **Restart Server**: Disable and re-enable MCP server
3. **Network**: Check internet connection stability
4. **System Resources**: Monitor CPU and memory usage

**中文**:
1. **关闭未使用文件**: 限制打开的Figma文件
2. **重启服务器**: 禁用并重新启用MCP服务器
3. **网络**: 检查互联网连接稳定性
4. **系统资源**: 监控CPU和内存使用情况

### Memory Usage | 内存使用

**English**:
1. **Figma Desktop**: Restart app if memory usage is high
2. **IDE Limits**: Some IDEs have context size limits
3. **Batch Requests**: Avoid multiple simultaneous requests

**中文**:
1. **Figma桌面**: 如果内存使用率高，重启应用
2. **IDE限制**: 某些IDE有上下文大小限制
3. **批量请求**: 避免多个同时请求

---

## Error Messages | 错误消息

### Common Error Codes | 常见错误代码

#### 403 Forbidden
**Cause | 原因**: Invalid or insufficient API permissions  
**Solution | 解决方案**: Regenerate API token with correct permissions

#### 404 Not Found
**Cause | 原因**: File or frame not found  
**Solution | 解决方案**: Verify Figma URL and access permissions

#### 429 Rate Limited
**Cause | 原因**: Too many requests  
**Solution | 解决方案**: Wait before making more requests

#### 500 Internal Server Error
**Cause | 原因**: Server-side issue  
**Solution | 解决方案**: Restart Figma Desktop, check file integrity

---

## Debug Mode | 调试模式

### Enable Detailed Logging | 启用详细日志

**For Community Servers | 对于社区服务器**:
```bash
npx figma-developer-mcp --figma-api-key=YOUR_KEY --debug --stdio
```

**For IDE Debugging | 对于IDE调试**:
- **Cursor**: Check Developer Tools (Cmd/Ctrl+Shift+I)
- **VS Code**: Check Output panel > MCP
- **Windsurf**: Check Debug console

---

## Getting Help | 获取帮助

### Official Resources | 官方资源
- [Figma Help Center](https://help.figma.com/) | [Figma帮助中心](https://help.figma.com/)
- [Figma Community](https://www.figma.com/community/) | [Figma社区](https://www.figma.com/community/)

### Community Support | 社区支持
- [GitHub Issues](../../issues) - Report problems
- [GitHub Discussions](../../discussions) - Ask questions
- [Discord Communities](https://discord.gg/figma) - Real-time help

### Before Asking for Help | 寻求帮助前

**English**: Please include:
1. Operating system and version
2. IDE name and version
3. Figma plan type
4. Complete error message
5. Configuration file (remove API tokens)
6. Steps to reproduce the issue

**中文**: 请包含：
1. 操作系统和版本
2. IDE名称和版本
3. Figma计划类型
4. 完整错误消息
5. 配置文件（删除API令牌）
6. 重现问题的步骤

---

*This troubleshooting guide is community-maintained. Please contribute improvements and additional solutions.*

*本故障排除指南由社区维护。请贡献改进和其他解决方案。*