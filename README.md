# DeepType-Theme

Its my custom theme for vscode inspired in the `sea`, `sunsets`, `rivers`, and `forests`.

Officially Language Support:
* javascript
* typescript
* powershell
* bash
* html
* css
* jsx/tsx
* json
* xml
* yml | yaml

## Development

### Testing the Extension Locally
Press `F5` in VSCode to open a new window with the extension loaded for testing.

### Building and Publishing

#### Prerequisites
Install the VSCode Extension Manager CLI:
```bash
npm install -g @vscode/vsce
```

#### Package the Extension
Create a `.vsix` file for local installation or distribution:
```bash
vsce package
```

This generates `deep-type-theme-{version}.vsix` that can be installed manually in VSCode.

#### Publish to VSCode Marketplace

1. **Create a Personal Access Token (PAT)**
   - Go to https://dev.azure.com/
   - Create a new organization if needed
   - Go to User Settings → Personal Access Tokens
   - Create a token with `Marketplace (Manage)` scope

2. **Login to vsce**
   ```bash
   vsce login {publisher-name}
   ```
   Enter your PAT when prompted.

3. **Publish the extension**
   ```bash
   vsce publish
   ```

   Or publish with a specific version bump:
   ```bash
   vsce publish patch  # 1.2.1 → 1.2.2
   vsce publish minor  # 1.2.1 → 1.3.0
   vsce publish major  # 1.2.1 → 2.0.0
   ```

4. **Verify Publication**
   - Visit https://marketplace.visualstudio.com/manage/publishers/{publisher-name}
   - Check your extension at https://marketplace.visualstudio.com/items?itemName=eythaann.deep-type-theme