## Publishing NPM Packages on GitHub
 This guide documents the steps to publish an NPM package on GitHub, including creating tokens, updating package.json, and resolving issues like GitHub Push Protection. Protytpe trial, not used, this is for training purpose only.

## Steps to Publish on GitHub Packages

1. Steps to Create a Token:

Go to GitHub Token Settings.
Click Generate new token (classic) or Create a new token (if using the fine-grained access option).
Select the permissions mentioned above.
Copy the generated token and store it securely


2. Set Up Authentication To publish an NPM package to GitHub, you need a Personal Access Token (PAT) with the following permissions:

write:packages
read:packages
delete:packages (if you want to delete packages later)
admin:repo_hook (if your repository is private)


### Update .npmrc File
To configure NPM to authenticate with GitHub:

Create a .npmrc file in the root of your project (or globally).

1. Add the following line:
@YOUR_USER_NAME_GITHUB:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=YOUR_PERSONAL_ACCESS_TOKEN

**Important:** Add `.npmrc` to `.gitignore` to avoid accidentally pushing it to the repository.

### 3. **Update `package.json`**


1. Set the name field to include your GitHub username:
  "name": "@username/example-package",            

3. Add the `repository` field to point to your GitHub repository:
  "repository": {
    "type": "git",
    "url": "https://github.com/username/example-repo.git"
  },

3. Add the publishConfig field to specify the registry:
  "publishConfig": {
    "registry": "https://npm.pkg.github.com/"
  },
  

### Publishing the Package
Login to NPM using the following command:

1. npm login --registry=https://npm.pkg.github.com/
Enter your GitHub username, email, and the token as the password.

2. If you are logged in to the specified registry, it will display your GitHub username.
npm whoami --registry=https://npm.pkg.github.com
If you are not logged in, you'll see an error then try again login

3. Build the Package Before publishing, ensure your package is built:
npm run build

2. Publish the package:
npm publish 
# If needed, explicitly specify the registry:
npm publish --registry=https://npm.pkg.github.com

3. Verify the package is available on GitHub by navigating to:
https://github.com/username?tab=packages

4. The npm show command can be used to retrieve information about your package hosted on GitHub Packages. Here’s how you can use it effectively:

npm show @username/hello-component --registry=https://npm.pkg.github.com


#### Note ****
If your .npmrc file already includes the GitHub token, you can skip the login step and directly build and publish the package.
