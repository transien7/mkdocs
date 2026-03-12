# Getting Started as a Python Developer


## Git

### Authentication

#### Creating an SSH key
1. Create a 2048-bit RSA key
```
ssh-keygen -b 2048 -t rsa
```
2. Save the key to `~/.ssh/github`
3. Add a password for additional security
4. Two keys will be created:
	* `github`: Your private key which should not be shared
	* `github.pub`: Your public key which should be uploaded to GitHub
5. Print the public key to the console
```
cat ~/.ssh/github.pub
```
6. Highlight and copy the entire public key for use in the next step

#### Updating SSH config to use the SSH key for GitHub
1. Modify the SSH config
```
vim ~/.ssh/config
```

2. Add the following to sign using your private key when authenticating to github.com
```
Host github.com
  User git
  IdentityFile ~/.ssh/github
```
3. Type `:wq` and press Enter to quit and write the changes

#### Adding SSH keys to GitHub
1. Go to [GitHub](https://github.com) and log in to your account
2. Click on the icon for your account in the top right and select `Settings`
3. Select `SSH and GPG keys` from the sidebar
4. Select `New SSH key`
5. Paste the output

### Creating a project
#### `git init`
Used to set up a local git repo. If or when you decide you want to push the repo to a remote repository on GitHub, you will need to

1. Create the repo on GitHub

2. Add the remote repo location.

With SSH authentication:
```
git remote add origin git@github.com:username/repo.git
```
 
 With HTTPS authentication:
```
git remote add origin https://github.com/username/repo.git
```

3. Push to the upstream repo
```
git push --set-upstream origin master
```

> If you know you'll be storing the repo remotely, it will be easier to create an empty repo on GitHub and then simply clone it locally

#### `git clone`


### Working on a project

#### `git status`


#### `git branch`, `git switch`, and `git checkout`


#### `git commit`


#### `git push`


#### `git merge`


## Formatting
#### Black Formatter


## Linting
#### Pylint



## Hooks
### pre-commit`


## Python Development

### Project Structure


### Packaging


## Containerisation

### Docker

#### Running containers
Containers can be run with a `docker-compose.yaml`.

#### Building container images
Containers can be built with a `Dockerfile`.

### Kubernetes
Container orchestration
#### Minikube
Local kubernetes environment

### Helm
Deployment management

