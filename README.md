## SSH-keys
* Want to push changes from local machine to github
* Secure version of http is https
* Want to change the protocol from https to ssh
* SSH is more secure 
* Authentication -> checking if youre allowed to carry out the action
* Can be authenticated with a username and password
* Can't use username and password with automation
* Can use keys
* Can use personel access token (it's a long string)
* Benefit of using SSH is that it uses keys, and keys are much longer -> makes it more secure
* Have to store key in secure place
* When the key is passed, it must be encrypted to protect the data
* Key's help with automation because once it is registered in the right place it will authenticate automatically.
* Want to push changes to github with ssh instead of HTTPS, need key pair for that
* Will use RSA key encryption
## Using SSH keys with github
1) Create SSH key pair, with RSA type
* Open gitbash
* Cd into .ssh
* Generate key : 
```
ssh-keygen -t rsa -b 4096 -C "email"
```
* Can use any email, doesn't have to be github email 
* Enter file into which youd like to save the key e.g:` github-key`
* Creates 2 files, one regular and one .pub
* 2 parts to RSA key -> padlock/public key and key/ private key
* Can keep the `.pub` public, its called a `public key`
* Keep the other key private, this is the `private key`
* Assymetric encryption system -> because theres a key pair, they are mathematically generated.
* Can generate a `public key` from the `private key`, cant generate a `private key` from the `public key`
* Symmetrical encryption - one key
* Will have to register public key on github
* On github its called an authentication key
* Encryption isn't relient on key, SSH is automatically encrypted
2) Add/register key on github account -> do this with public key
* Open gitbuh
* Click on your profile picture in the top right corner, and select settings
* Click `SSH and GPG keys`
* Name your key
* Go into gitbash, print you public key with `cat`
* Copy the entire key, email included
* Paste it into the box
* Click add key
* Confirm with password and 2-factor authentication if needed.
* So far we have registered the public key with github
3) Add private key to ssh private key list
* Need to start ssh-agent:
```
eval `ssh-agent -s`
```
* Displayes the process ID
* Run:
``` 
ssh-add github-key
```
* Should output identity added, followed by email address
* Test if the key registered by ssh is used to authenticate to github:
```
ssh -T git@github.com
```
* Will now automatically use private key to automatically authenticate to github
4) Create test repository on github
5) Push changes to github using SSH key
* `git init` creates a hidden folder with hidden files -> initialises your working directory as a git directory
* The hidden folders do the following:
* Keep track of `commits`
* Keep track of `staging`
* `git add` adding it to staging -> git starts tracking files
* `git status` - shows what files are staged and committed.
* `git commit -m "message"` - readies the staged files for pushing
* `git branch -M main`- create a branch called `main`
* `git remote add origin git@github.com:gitrepo` - specifies the path to a selected remote repository
* `git push -u origin main` - pushes changes to the repository
* ` 
* Origin - where it comes from
* Specifying the ssh version of where the repository is remotely
* Once a key has been registered, its put in its own secure location.
* Even if the `private key` is moved around, it should still work
* Protocol is like a language used to push changes
* HTTPS and SSH both secure
* Once you've pushed your changes to any branch, dont need to specify the branch, pushes will default to the most recently used branch

![](images/ssh_github.png)

## Switching back to HTTPS
* `git remote remove origin`
* `git remote add origin https_link`
## SSH vs HTTPS
* SSH is more secure
* Once SSH is registered, dont have to enter it again, therefore good for automation
## Potential issues -> permission denied
* If you open another gitbash terminal and try to push your changes from there while the original terminal is open, it will not work. You will be denied permission, so ensure that you only attempt to push changes from the terminal where you used 
```
eval `ssh-agent -s`
```
and
```
ssh-add github-key
```
* If you are unsure whether you have permissions in your current terminal, run :
```
ssh -T git@github.com
```