# Publishing Instructions for servify-express

This document describes how to publish the `@aarondoran/servify-express` package to both npmjs.org and GitHub Packages.

## ✅ Configuration Complete

The following files have been configured correctly:

### 1. package.json
- **Scope**: `@aarondoran` (matching GitHub Packages namespace)
- **Version**: `1.1.2` (ready for new release)
- **Test script**: Configured to prevent npm failures

### 2. .npmrc
- Configures the `@aarondoran` scope to use GitHub Packages registry
- Authentication is handled by the GitHub Actions workflow

### 3. GitHub Actions Workflow (.github/workflows/publish.yml)
- **Trigger**: Runs on release creation
- **Steps**:
  1. Checks out code
  2. Sets up Node.js for npmjs registry
  3. Installs dependencies with `npm ci`
  4. Publishes to npmjs with `--access public` using `NPM_TOKEN` secret
  5. Sets up Node.js for GitHub Packages registry
  6. Publishes to GitHub Packages with `--access public` using `GITHUB_TOKEN` secret

## 📋 Prerequisites

Before creating a release, ensure the following secrets are configured in your repository:

### NPM_TOKEN
1. Go to https://www.npmjs.com/
2. Login and navigate to **Access Tokens** in your account settings
3. Create a new **Automation** token (or **Classic** token with publish permissions)
4. Copy the token
5. Go to https://github.com/Aarondoran/servify-express/settings/secrets/actions
6. Create a new secret named `NPM_TOKEN` and paste the token value

### GITHUB_TOKEN
- This is automatically provided by GitHub Actions
- No manual configuration needed
- Ensure your repository has **Workflow permissions** set correctly:
  - Go to https://github.com/Aarondoran/servify-express/settings/actions
  - Under "Workflow permissions", ensure "Read and write permissions" is selected

## 🚀 Creating a Release

To trigger the publishing workflow:

1. **Via GitHub UI**:
   - Go to https://github.com/Aarondoran/servify-express/releases/new
   - **Tag**: `v1.1.2` (or `V1.1.2` to match your existing convention)
   - **Target**: Select `main` branch
   - **Release title**: `v1.1.2` or a descriptive name
   - **Description**: Add release notes describing changes
   - Click **Publish release**

2. **Via Git CLI** (if you have push access):
   ```bash
   git checkout main
   git pull origin main
   git tag -a v1.1.2 -m "Release version 1.1.2"
   git push origin v1.1.2
   # Then create the release on GitHub from this tag
   ```

3. **Via GitHub CLI**:
   ```bash
   gh release create v1.1.2 --title "v1.1.2" --notes "Fixed npm publishing workflow"
   ```

## 🔍 Verifying the Workflow

After creating the release:

1. **Monitor the workflow**:
   - Go to https://github.com/Aarondoran/servify-express/actions
   - You should see a "Publish Node Package" workflow running
   - Wait for it to complete successfully (green checkmark)

2. **Check for errors**:
   - If the workflow fails, click on it to see the logs
   - Common issues:
     - Missing or invalid `NPM_TOKEN` secret
     - Insufficient GitHub token permissions
     - Package version already published

## ✅ Verifying Package Installation

Once the workflow completes successfully, verify the package can be installed from both registries:

### From npmjs.org:
```bash
# In a new directory
npm install @aarondoran/servify-express

# Test it works
node -e "const StartServer = require('@aarondoran/servify-express'); console.log('Loaded:', typeof StartServer.listen)"
```

### From GitHub Packages:
```bash
# Create a .npmrc file with authentication
echo "@aarondoran:registry=https://npm.pkg.github.com" > .npmrc
echo "//npm.pkg.github.com/:_authToken=YOUR_GITHUB_TOKEN" >> .npmrc

# Install the package
npm install @aarondoran/servify-express

# Test it works
node -e "const StartServer = require('@aarondoran/servify-express'); console.log('Loaded:', typeof StartServer.listen)"
```

**Note**: For GitHub Packages, you need a GitHub Personal Access Token with `read:packages` scope.

## 📦 Package URLs

After successful publication:

- **npmjs**: https://www.npmjs.com/package/@aarondoran/servify-express
- **GitHub Packages**: https://github.com/Aarondoran/servify-express/packages

## 🔄 Future Releases

For future releases:

1. Update the version in `package.json`:
   ```bash
   npm version patch  # for 1.1.3
   npm version minor  # for 1.2.0
   npm version major  # for 2.0.0
   ```

2. Commit the version change:
   ```bash
   git add package.json package-lock.json
   git commit -m "Bump version to X.Y.Z"
   git push origin main
   ```

3. Create a new release following the steps above

## 🐛 Troubleshooting

### Workflow fails with authentication error
- Verify `NPM_TOKEN` secret is set correctly
- Ensure the npm token has not expired
- Check token has publish permissions

### Package already exists error
- Update the version number in `package.json`
- Cannot republish the same version

### GitHub Packages authentication fails
- Verify workflow has `packages: write` permission (already configured)
- Check repository settings allow workflow to write packages

## 📝 Summary of Changes

The workflow has been fixed to:
- Use `actions/setup-node@v4` with proper `registry-url` configuration for each registry
- Use `NPM_TOKEN` secret for npmjs (not `NODE_AUTH_TOKEN`)
- Use `GITHUB_TOKEN` secret for GitHub Packages
- Add `--access public` flag to both publish commands for consistency
- Properly configure the scope `@aarondoran` for GitHub Packages
