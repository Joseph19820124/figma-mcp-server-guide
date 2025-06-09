# Complete Guide to Figma MCP Server

## Table of Contents
1. [Introduction](#introduction)
2. [What is Figma MCP Server?](#what-is-figma-mcp-server)
3. [Prerequisites and Requirements](#prerequisites-and-requirements)
4. [Pricing and Plans](#pricing-and-plans)
5. [Installation and Setup](#installation-and-setup)
6. [Configuration for Different IDEs](#configuration-for-different-ides)
7. [Usage and Best Practices](#usage-and-best-practices)
8. [Troubleshooting](#troubleshooting)
9. [Alternatives](#alternatives)
10. [FAQ](#faq)

---

## Introduction

Figma's Dev Mode MCP Server represents a significant leap forward in design-to-development workflows. Released in beta, this tool bridges the gap between design and code by providing AI-powered development tools with direct access to Figma design data.

The Model Context Protocol (MCP) is an open standard that allows AI applications to connect to various data sources and tools. Figma's implementation of this protocol enables developers to bring design context directly into their coding environment, resulting in more accurate and efficient code generation.

---

## What is Figma MCP Server?

### Core Functionality
The Figma Dev Mode MCP Server is a local server that runs on your machine and provides AI coding tools with:

- **Design Specifications**: Access to exact measurements, colors, typography, and spacing
- **Component Information**: Details about design components, their properties, and variants
- **Design Variables**: Access to design tokens, color schemes, and text styles
- **Layout Data**: Information about positioning, constraints, and responsive behavior
- **Asset Information**: Details about images, icons, and other design assets

### How It Works
1. **Local Server**: Runs locally at `http://127.0.0.1:3845/sse`
2. **MCP Protocol**: Uses standardized communication with AI tools
3. **Real-time Access**: Provides live data from your Figma designs
4. **Selective Context**: Allows configuration of what information to share

---

## Prerequisites and Requirements

### Account Requirements
- **Figma Account**: Professional, Organization, or Enterprise plan
- **Seat Type**: Dev or Full seat required
- **Desktop App**: Must use Figma desktop application (web version not supported)

### Technical Requirements
- **Operating System**: Windows, macOS, or Linux
- **Development Environment**: 
  - VS Code with GitHub Copilot
  - Cursor
  - Windsurf
  - Claude Code
  - Zed (with MCP support)
- **API Access**: Figma API access token with appropriate permissions

### Skills Required
- Basic understanding of development workflows
- Familiarity with your chosen IDE
- Basic knowledge of JSON configuration
- Understanding of API tokens and security

---

## Pricing and Plans

### Official Figma Plans

#### Professional Plan
- **Cost**: ~$15 per editor/month, ~$15 per dev/month
- **Dev Mode Access**: ✅ Available
- **Features**: 
  - Full design and dev mode access
  - No distinction between editor and dev seats
  - All dev mode features included
  - MCP server access included

#### Organization Plan  
- **Cost**: ~$45 per editor/month, variable for dev seats
- **Dev Mode Access**: ✅ Available with dedicated dev seats
- **Features**:
  - Separate pricing for dev-only seats
  - Advanced collaboration features
  - Organization-level controls
  - Priority support

#### Enterprise Plan
- **Cost**: Custom pricing, ~$35/month for dev seats
- **Dev Mode Access**: ✅ Available with enhanced features
- **Features**:
  - Dedicated dev seats at $35/month
  - Advanced security and governance
  - Custom integrations
  - White-glove support

### Cost Considerations

#### For Small Teams (1-5 developers)
- **Professional Plan**: Most cost-effective option
- **Total Cost**: $75-225/month for team access
- **Recommendation**: Start with Professional plan

#### For Medium Teams (5-20 developers)
- **Organization Plan**: Better dev seat pricing
- **Total Cost**: $200-800/month depending on mix
- **Recommendation**: Consider Organization plan for dev seat savings

#### For Large Teams (20+ developers)
- **Enterprise Plan**: Volume discounts and dedicated dev seats
- **Total Cost**: Negotiable based on usage
- **Recommendation**: Enterprise plan with dedicated dev seats

### Free Alternatives
- **Community MCP Servers**: Free but require technical setup
- **Third-party Solutions**: Various pricing models available
- **API Direct Access**: Free tier available with limitations

---

## Installation and Setup

### Step 1: Enable Dev Mode MCP Server in Figma

1. **Download Figma Desktop App**
   - Visit [figma.com/downloads](https://www.figma.com/downloads)
   - Download and install the desktop application
   - Log in with your Figma account

2. **Enable MCP Server**
   - Open Figma Desktop
   - Go to **Help and Account** > **Preferences**
   - Find **Dev Mode** section
   - Toggle **Enable Dev Mode MCP Server**
   - Note the server address: `http://127.0.0.1:3845/sse`

### Step 2: Generate Figma API Token (for third-party servers)

1. **Access Account Settings**
   - Go to [figma.com/settings](https://www.figma.com/settings)
   - Navigate to **Security** tab

2. **Create Access Token**
   - Click **Create new token**
   - Name your token (e.g., "MCP Server Token")
   - Select permissions:
     - **File content**: Read access
     - **Dev resources**: Read access
     - **Comments**: No access (recommended)
     - **Team library**: Read access (if needed)

3. **Save Token Securely**
   - Copy the token immediately (shown only once)
   - Store in a secure location (password manager recommended)
   - Never commit tokens to version control

---

## Configuration for Different IDEs

### Cursor Configuration

#### Method 1: Official Figma MCP Server
1. **Open Cursor Settings**
   - `Cursor` > `Settings` > `Cursor Settings`
   - Navigate to **MCP** tab

2. **Add Server**
   - Click **+ Add new global MCP server**
   - **Name**: `Figma Dev Mode MCP`
   - **Type**: `sse`
   - **URL**: `http://127.0.0.1:3845/sse`

3. **Enable Agent Mode**
   - Open chat toolbar (`⌥⌘B`)
   - Switch to **Agent mode**
   - Look for **MCP Server: Figma Dev Mode MCP** in tools

#### Method 2: Community MCP Server
```json
{
  "mcpServers": {
    "Figma": {
      "command": "npx",
      "args": ["-y", "figma-developer-mcp", "--figma-api-key=YOUR_TOKEN", "--stdio"]
    }
  }
}
```

### VS Code Configuration

1. **Prerequisites**
   - Install GitHub Copilot extension
   - Enable GitHub Copilot Chat

2. **Settings Configuration**
   - Open **Command Palette** (`Cmd/Ctrl + Shift + P`)
   - Search for "MCP"
   - Select **Edit in settings.json**

3. **Add Configuration**
```json
{
  "chat.mcp.discovery.enabled": true,
  "mcp": {
    "servers": {
      "Figma Dev Mode MCP": {
        "type": "sse",
        "url": "http://127.0.0.1:3845/sse"
      }
    }
  },
  "chat.agent.enabled": true
}
```

### Windsurf Configuration

1. **Open Settings**
   - `Windsurf` > `Settings` > `Windsurf Settings`
   - Or use shortcut `⌘ ,`

2. **Install Plugin**
   - Navigate to **Cascade settings**
   - Select **Open plugin store**
   - Search for "Figma"
   - Install the Figma plugin

3. **Configuration Note**
   - Change `url` property to `serverUrl` in configuration
   - This prevents common configuration errors

### Claude Code Configuration

Claude Code supports MCP natively and will auto-detect running MCP servers on your local machine.

1. **Install Claude Code**
   - Follow installation instructions from Anthropic
   - Ensure MCP support is enabled

2. **Auto-detection**
   - Claude Code will automatically detect the Figma MCP server
   - No manual configuration required

---

## Usage and Best Practices

### Getting Started

#### Basic Workflow
1. **Open Your Design in Figma**
   - Use Figma Desktop app (required)
   - Ensure MCP server is running

2. **Start Your IDE**
   - Open your preferred IDE with MCP support
   - Activate agent/AI mode

3. **Reference Your Design**
   - Copy Figma frame/component URL
   - Paste in AI chat
   - Ask for implementation

#### Example Prompts
```
"Using the Figma MCP, implement this design: [Figma URL]"

"Analyze the design at [Figma URL] and create a React component"

"Generate CSS for the layout shown in this Figma frame: [URL]"

"Extract the design tokens from this Figma file: [URL]"
```

### Best Practices

#### Design Preparation
1. **Organize Your Designs**
   - Use clear naming conventions
   - Group related elements
   - Create consistent component structures

2. **Prepare Components**
   - Detach instances if having issues
   - Use frames instead of groups when possible
   - Ensure proper layer hierarchy

3. **Design System Alignment**
   - Use consistent variables and styles
   - Align design tokens with code tokens
   - Document component usage patterns

#### Development Workflow
1. **Iterative Approach**
   - Start with basic layout
   - Refine details in iterations
   - Test across different screen sizes

2. **Context Management**
   - Provide clear, specific prompts
   - Include relevant codebase context
   - Specify framework and styling preferences

3. **Quality Control**
   - Review generated code thoroughly
   - Test responsive behavior
   - Validate accessibility features

### Advanced Usage

#### Custom Configuration
- Adjust MCP server settings for specific context needs
- Configure IDE-specific preferences
- Set up project-specific workflows

#### Integration with Design Systems
- Map Figma variables to code tokens
- Automate component library updates
- Sync design changes with code repositories

---

## Troubleshooting

### Common Issues

#### Server Connection Problems
**Issue**: MCP client cannot connect to Figma server
**Solutions**:
- Ensure Figma Desktop is running
- Verify MCP server is enabled in preferences
- Check that no firewall is blocking port 3845
- Restart Figma Desktop app

#### Authentication Errors
**Issue**: API token authentication failures
**Solutions**:
- Verify token has correct permissions
- Check token hasn't expired
- Ensure token is correctly configured
- Regenerate token if necessary

#### Component Reading Issues
**Issue**: MCP server cannot read certain components
**Solutions**:
- Detach component instances
- Convert groups to frames
- Simplify complex nested structures
- Check for corrupted design elements

#### IDE Configuration Problems
**Issue**: IDE doesn't recognize MCP server
**Solutions**:
- Verify IDE supports MCP protocol
- Check configuration file syntax
- Restart IDE after configuration changes
- Clear IDE cache if necessary

### Performance Optimization

1. **Reduce Context Size**
   - Limit scope of design queries
   - Use specific frame references
   - Avoid querying entire large files

2. **Network Optimization**
   - Ensure stable internet connection
   - Use local caching when available
   - Minimize concurrent requests

3. **Resource Management**
   - Close unused Figma files
   - Restart server periodically
   - Monitor system resources

---

## Alternatives

### Community Solutions

#### Figma-Context-MCP by GLips
- **Repository**: [GitHub](https://github.com/GLips/Figma-Context-MCP)
- **Features**: Simplified context for better accuracy
- **Cost**: Free
- **Setup**: Requires manual configuration

#### Figma-MCP-Server by TimHolden
- **Repository**: [GitHub](https://github.com/TimHolden/figma-mcp-server)
- **Features**: Full TypeScript implementation
- **Cost**: Free
- **Setup**: Advanced configuration options

### Third-party Solutions

#### Builder.io
- **Features**: Advanced design-to-code workflows
- **Cost**: Paid service with free tier
- **Integration**: Direct Figma integration

#### Anima
- **Features**: Design-to-code automation
- **Cost**: Subscription-based
- **Integration**: Figma plugin

#### Locofy
- **Features**: React/React Native code generation
- **Cost**: Freemium model
- **Integration**: Direct export from Figma

---

## FAQ

### General Questions

**Q: Is Figma MCP Server free?**
A: The MCP server itself is included with paid Figma plans, but you need a Professional, Organization, or Enterprise plan with Dev or Full seats.

**Q: Can I use it with the free Figma plan?**
A: No, Dev Mode and MCP server access require paid plans.

**Q: Does it work with Figma in the browser?**
A: No, you must use the Figma Desktop application.

### Technical Questions

**Q: Which IDEs are supported?**
A: Currently supports Cursor, VS Code (with Copilot), Windsurf, Claude Code, and Zed.

**Q: Can I use it with multiple projects?**
A: Yes, the server can access any Figma file you have permission to view.

**Q: Is my design data secure?**
A: Yes, the server runs locally and only shares data with your configured MCP clients.

### Pricing Questions

**Q: What's the most cost-effective plan for developers?**
A: For small teams, Professional plan is usually most cost-effective. For larger teams, Enterprise plan with dedicated dev seats at $35/month may be better.

**Q: Are there any hidden costs?**
A: No hidden costs, but you may need to factor in IDE subscriptions (like GitHub Copilot for VS Code).

**Q: Can I try it for free?**
A: Figma offers trials for paid plans, and you can use community MCP servers for free with API tokens.

---

*This guide is maintained by the community and updated regularly. For the latest information, always refer to Figma's official documentation.*