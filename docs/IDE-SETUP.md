# IDE Setup Guide

This guide provides detailed instructions for setting up and using Awesome GitHub Copilot resources (agents, prompts, instructions, and skills) across different Integrated Development Environments (IDEs).

## Table of Contents

- [Overview](#overview)
- [Visual Studio Code](#visual-studio-code)
- [Visual Studio](#visual-studio)
- [Other IDEs](#other-ides)
- [MCP Server Configuration](#mcp-server-configuration)
- [Feature Comparison](#feature-comparison)
- [Troubleshooting](#troubleshooting)

## Overview

Awesome GitHub Copilot provides a collection of customizations to enhance your GitHub Copilot experience. The installation and usage methods vary by IDE. This guide helps you set up and use these resources effectively regardless of your development environment.

### What You Can Install

- **Agents** (`.agent.md`) - Specialized GitHub Copilot agents for specific workflows
- **Prompts** (`.prompt.md`) - Task-specific prompts for code generation
- **Instructions** (`.instructions.md`) - Coding standards that apply to file patterns
- **Skills** - Self-contained capability bundles with resources
- **Collections** - Curated sets of related resources

## Visual Studio Code

VS Code has the most mature integration with GitHub Copilot customizations and offers the best user experience.

### Prerequisites

- [Visual Studio Code](https://code.visualstudio.com/) or [VS Code Insiders](https://code.visualstudio.com/insiders/)
- [GitHub Copilot Extension](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot)
- [GitHub Copilot Chat Extension](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat)

### Installation Methods

#### Method 1: One-Click Installation (Recommended)

Throughout this repository, you'll find install buttons for individual resources:

[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install-0098FF?logo=visualstudiocode&logoColor=white)](https://aka.ms/awesome-copilot/mcp/vscode)

Simply click these buttons to install the resource directly into VS Code.

#### Method 2: Manual Installation

1. **Download the file** you want to use (e.g., `example.agent.md`)
2. **Place it in your workspace:**
   - For workspace-specific: Create a `.github/copilot/` directory in your project root
   - For user-wide: Place in your VS Code user settings directory
3. **The resource will be automatically detected** by GitHub Copilot

Example directory structure:
```
your-project/
├── .github/
│   └── copilot/
│       ├── agents/
│       │   └── custom-agent.agent.md
│       ├── prompts/
│       │   └── custom-prompt.prompt.md
│       └── instructions/
│           └── custom.instructions.md
└── src/
```

#### Method 3: MCP Server (Advanced)

Install and configure the Awesome Copilot MCP server to browse and install resources dynamically:

1. **Ensure Docker is installed and running**
2. **Open VS Code Settings** (`Ctrl/Cmd + ,`)
3. **Search for** "MCP Servers"
4. **Add the Awesome Copilot MCP server configuration:**

```json
{
  "github.copilot.chat.mcp.servers": {
    "awesome-copilot": {
      "type": "stdio",
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "ghcr.io/microsoft/mcp-dotnet-samples/awesome-copilot:latest"
      ]
    }
  }
}
```

5. **Reload VS Code** to activate the server
6. **Use the search prompt** in Copilot Chat to find and install resources

### Using Resources in VS Code

#### Agents
- **Activate via Chat:** Type `@agent-name` in the Copilot Chat panel
- **Select from UI:** Use the agent picker in the Chat interface
- **For CCA:** Select the agent when assigning issues to Copilot

#### Prompts
- **Use slash commands:** Type `/prompt-name` in Copilot Chat
- **Browse available prompts:** Type `/` to see all installed prompts

#### Instructions
- **Automatic application:** Instructions apply automatically based on file patterns
- **No manual activation needed**

#### Skills
- **Automatic integration:** Skills are available to agents once installed
- **Referenced by agents:** Check agent documentation for skill requirements

### VS Code Tips

- Use `Ctrl/Cmd + Shift + P` and search for "Copilot" to see all available commands
- Access Copilot Chat via the sidebar or `Ctrl/Cmd + I`
- View installed agents in the agent picker (click the `@` symbol in Chat)

## Visual Studio

Visual Studio (full IDE) has GitHub Copilot support but with a different integration model compared to VS Code.

### Prerequisites

- [Visual Studio 2022](https://visualstudio.microsoft.com/) (version 17.8 or later recommended)
- [GitHub Copilot Extension for Visual Studio](https://marketplace.visualstudio.com/items?itemName=GitHub.copilotvs)

### Current Limitations

Visual Studio's GitHub Copilot integration is evolving and has some differences from VS Code:

- **Limited Custom Agent UI:** No visual agent picker like VS Code
- **Different Chat Interface:** Integrated but with fewer customization options
- **File-based Configuration:** Relies on file-based customization in workspace

### Installation Methods

#### Method 1: Manual File Installation (Primary Method)

This is currently the most reliable method for Visual Studio:

1. **Create the `.github/copilot/` directory** in your solution root:
   ```
   YourSolution/
   ├── .github/
   │   └── copilot/
   │       ├── agents/
   │       ├── prompts/
   │       └── instructions/
   └── YourProject/
   ```

2. **Download and place files** in the appropriate subdirectories:
   - Agents → `.github/copilot/agents/`
   - Prompts → `.github/copilot/prompts/`
   - Instructions → `.github/copilot/instructions/`

3. **Reload or restart Visual Studio** to ensure changes are detected

4. **Verify installation** by opening the Copilot Chat window

#### Method 2: MCP Server Configuration

Visual Studio supports MCP servers through configuration:

1. **Ensure Docker is installed and running**

2. **Create or edit the MCP configuration file:**
   - Location: `%APPDATA%\GitHub Copilot\config.json` (Windows)
   - Location: `~/.config/github-copilot/config.json` (macOS/Linux)

3. **Add the Awesome Copilot server configuration:**

```json
{
  "mcpServers": {
    "awesome-copilot": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "ghcr.io/microsoft/mcp-dotnet-samples/awesome-copilot:latest"
      ]
    }
  }
}
```

4. **Restart Visual Studio** to load the MCP server

5. **Access MCP features** through the Copilot Chat interface

#### Method 3: One-Click Installation (When Available)

Some resources in this repository have install buttons for Visual Studio:

[![Install in Visual Studio](https://img.shields.io/badge/Visual_Studio-Install-C16FDE?logo=visualstudio&logoColor=white)](https://aka.ms/awesome-copilot/mcp/vs)

Click these buttons to attempt automatic installation.

### Using Resources in Visual Studio

#### Agents
- **Access via Chat:** Type questions in the Copilot Chat window
- **Agent selection may be implicit** based on context and installed agents
- **For specific agents:** Mention the agent name in your chat prompt

#### Prompts
- **May need to be invoked manually** by copying content or referencing in chat
- **Watch for future Visual Studio updates** that improve prompt integration

#### Instructions
- **Automatic application:** Instructions apply based on file patterns
- **Work similarly to VS Code**

### Visual Studio Tips

- **Enable Copilot Chat:** View → GitHub Copilot Chat
- **Keep Visual Studio updated:** Newer versions have better Copilot integration
- **Check for extension updates:** GitHub regularly improves the Visual Studio extension
- **Use Solution Explorer:** Right-click on files for Copilot context menu options

### Known Differences from VS Code

| Feature | VS Code | Visual Studio |
|---------|---------|---------------|
| Agent Picker UI | ✅ Visual interface | ⚠️ Limited/text-based |
| Slash Commands for Prompts | ✅ Full support | ⚠️ Partial support |
| Automatic Instruction Detection | ✅ Yes | ✅ Yes |
| MCP Server Support | ✅ Full support | ✅ Supported |
| One-Click Install | ✅ Seamless | ⚠️ May require manual steps |
| Custom Agent Selection | ✅ Easy UI | ⚠️ Text-based/implicit |

## Other IDEs

GitHub Copilot is available in several IDEs, but custom agent/prompt/instruction support varies.

### JetBrains IDEs (IntelliJ, Rider, PyCharm, etc.)

**Status:** GitHub Copilot is available as a plugin, but custom agent/prompt/instruction support is limited.

**Current Capabilities:**
- ✅ GitHub Copilot inline suggestions
- ✅ Copilot Chat
- ⚠️ Limited custom instruction support
- ❌ Custom agents not fully supported
- ❌ Custom prompts may not work

**Recommended Approach:**
- Use GitHub Copilot for code suggestions
- Consider using VS Code alongside for custom agents/prompts
- Watch for JetBrains plugin updates

**Installation:**
1. Install GitHub Copilot plugin from JetBrains Marketplace
2. Attempt to add `.github/copilot/` directory with instructions
3. Some file-based customizations may work

### Neovim

**Status:** GitHub Copilot support via plugins, custom extensions possible with advanced configuration.

**Popular Plugins:**
- [copilot.vim](https://github.com/github/copilot.vim)
- [copilot.lua](https://github.com/zbirenbaum/copilot.lua)

**Custom Resources:**
- May require manual integration
- Community plugins exist for extended functionality

### Other Editors

- **Sublime Text:** Limited via plugin
- **Emacs:** Via copilot.el plugin
- **Eclipse:** Check for GitHub Copilot extension

**General Advice for Other IDEs:**
1. Check if the IDE has official GitHub Copilot support
2. Look for community extensions that add customization support
3. Use file-based configurations in `.github/copilot/` directory
4. Consider running VS Code in parallel for access to full agent capabilities

## MCP Server Configuration

The Model Context Protocol (MCP) server enables dynamic discovery and installation of resources.

### What is MCP?

MCP (Model Context Protocol) is a protocol that allows AI systems to connect to external data sources and tools. The Awesome Copilot MCP server provides search and installation capabilities for resources in this repository.

### Prerequisites

- Docker installed and running
- GitHub Copilot Chat installed in your IDE
- Network access to pull Docker images

### Configuration by IDE

#### VS Code / VS Code Insiders

Add to `.vscode/settings.json` or user settings:

```json
{
  "github.copilot.chat.mcp.servers": {
    "awesome-copilot": {
      "type": "stdio",
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "ghcr.io/microsoft/mcp-dotnet-samples/awesome-copilot:latest"
      ]
    }
  }
}
```

#### Visual Studio

Create/edit `%APPDATA%\GitHub Copilot\config.json`:

```json
{
  "mcpServers": {
    "awesome-copilot": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "ghcr.io/microsoft/mcp-dotnet-samples/awesome-copilot:latest"
      ]
    }
  }
}
```

### Using the MCP Server

Once configured:

1. Open Copilot Chat
2. Use search prompts to find resources:
   - "Search for Python agents"
   - "Find security-related instructions"
   - "Install the React expert agent"
3. The MCP server will search the repository and help install resources

### Custom MCP Server Configuration

You can pass custom arguments to the MCP server:

```json
{
  "type": "stdio",
  "command": "docker",
  "args": [
    "run",
    "-i",
    "--rm",
    "-e", "INSTALL_PATH=/custom/path",
    "ghcr.io/microsoft/mcp-dotnet-samples/awesome-copilot:latest"
  ]
}
```

**Potential environment variables:**
- `INSTALL_PATH`: Customize where resources are installed
- Add IDE-specific configuration as the server evolves

## Feature Comparison

### IDE Feature Matrix

| Feature | VS Code | Visual Studio | JetBrains | Neovim | Other |
|---------|---------|---------------|-----------|--------|-------|
| **Core Copilot** | ✅ | ✅ | ✅ | ⚠️ | Varies |
| **Custom Agents** | ✅ Full | ⚠️ Limited | ❌ | ❌ | ❌ |
| **Custom Prompts** | ✅ Full | ⚠️ Partial | ❌ | ❌ | ❌ |
| **Custom Instructions** | ✅ Full | ✅ Good | ⚠️ Limited | ❌ | ❌ |
| **Skills Support** | ✅ Full | ⚠️ Limited | ❌ | ❌ | ❌ |
| **MCP Servers** | ✅ Full | ✅ Full | ❌ | ❌ | ❌ |
| **One-Click Install** | ✅ | ⚠️ | ❌ | ❌ | ❌ |
| **Agent Picker UI** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **Slash Commands** | ✅ | ⚠️ | ⚠️ | ❌ | ❌ |

**Legend:**
- ✅ Full support
- ⚠️ Partial/limited support
- ❌ Not supported or unknown

### Recommendations by Use Case

**Best Overall Experience:**
- Use **Visual Studio Code** for the most complete feature set

**C#/.NET Development:**
- **Visual Studio** is excellent for the IDE experience
- Use `.github/copilot/` directory for custom instructions
- Consider VS Code alongside for advanced agent features

**Java/Kotlin Development:**
- **IntelliJ IDEA** for the IDE
- Manual instruction files may work
- Use VS Code for custom agents

**Multi-Language/General:**
- **VS Code** provides the best cross-language support

## Troubleshooting

### General Issues

#### Resources Not Appearing

**Problem:** Installed agents/prompts don't show up

**Solutions:**
1. Verify files are in the correct directory (`.github/copilot/`)
2. Check file extensions (.agent.md, .prompt.md, .instructions.md)
3. Restart your IDE
4. Ensure GitHub Copilot extensions are up to date
5. Check that frontmatter is properly formatted

#### MCP Server Not Working

**Problem:** MCP server doesn't connect

**Solutions:**
1. Verify Docker is running: `docker ps`
2. Test Docker connectivity: `docker pull ghcr.io/microsoft/mcp-dotnet-samples/awesome-copilot:latest`
3. Check configuration file syntax (valid JSON)
4. Review IDE logs for MCP connection errors
5. Restart IDE after configuration changes

### VS Code Specific

#### Agent Not in Picker

**Problem:** Custom agent doesn't appear in @ menu

**Solutions:**
1. Check file location: `.github/copilot/agents/your-agent.agent.md`
2. Verify frontmatter has required fields
3. Reload window: `Ctrl/Cmd + Shift + P` → "Developer: Reload Window"
4. Check for syntax errors in the agent file

#### Slash Command Not Working

**Problem:** Custom prompt doesn't work with `/command`

**Solutions:**
1. Ensure file is in `.github/copilot/prompts/`
2. Check that frontmatter includes `agent: 'agent'`
3. Verify the prompt has a `description` field
4. Restart Copilot Chat

### Visual Studio Specific

#### Chat Window Not Opening

**Problem:** Copilot Chat doesn't appear

**Solutions:**
1. Ensure GitHub Copilot extension is installed
2. Check Visual Studio version (17.8+ recommended)
3. View → GitHub Copilot Chat
4. Restart Visual Studio
5. Repair/reinstall GitHub Copilot extension

#### Custom Resources Not Loading

**Problem:** Instructions or agents don't work

**Solutions:**
1. Verify `.github/copilot/` directory exists in solution root
2. Check that files have correct extensions
3. Ensure frontmatter is valid
4. Clean and rebuild solution
5. Close and reopen files to trigger Copilot context refresh

#### MCP Configuration Not Found

**Problem:** MCP server config not recognized

**Solutions:**
1. Check config file location:
   - Windows: `%APPDATA%\GitHub Copilot\config.json`
   - macOS: `~/.config/github-copilot/config.json`
2. Verify JSON syntax is valid
3. Ensure proper permissions on config file
4. Restart Visual Studio after changes

### JetBrains IDEs

#### Limited Customization

**Issue:** Custom agents/prompts not supported

**Workaround:**
1. Use file-based instructions (may work)
2. Run VS Code in parallel for agent features
3. Wait for plugin updates
4. Check JetBrains marketplace for community plugins

### Docker Issues

#### Docker Not Running

**Problem:** MCP server fails to start

**Solutions:**
1. Start Docker Desktop
2. Verify with: `docker ps`
3. Check Docker is in PATH
4. Restart Docker service

#### Image Pull Failures

**Problem:** Can't download MCP server image

**Solutions:**
1. Check network connectivity
2. Verify Docker Hub access
3. Try manual pull: `docker pull ghcr.io/microsoft/mcp-dotnet-samples/awesome-copilot:latest`
4. Check corporate firewall settings
5. Use alternative registry if needed

## Getting Help

If you encounter issues not covered here:

1. **Check the repository:** [Awesome GitHub Copilot Issues](https://github.com/github/awesome-copilot/issues)
2. **Review official docs:** 
   - [VS Code Copilot Customization](https://code.visualstudio.com/docs/copilot/copilot-customization)
   - [GitHub Copilot Documentation](https://docs.github.com/copilot)
3. **Open an issue:** Describe your IDE, OS, and specific problem
4. **Community support:** See [SUPPORT.md](../SUPPORT.md)

## Contributing IDE-Specific Documentation

If you've successfully set up Awesome Copilot resources in an IDE not fully covered here:

1. Document your process
2. Open a pull request with updates to this guide
3. Share configuration examples
4. Help others in your IDE community

See [CONTRIBUTING.md](../CONTRIBUTING.md) for contribution guidelines.

---

**Last Updated:** 2026-02-06

**Feedback:** Please open an issue if you find any errors or have suggestions for improving this guide.
