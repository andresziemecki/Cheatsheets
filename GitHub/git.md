# Git

## Set up your git account in a new notebook

``` bash
sudo pacman -Syu # update machine
sudo pacman -S git # install git
git --version # check the installation
git config --global user.name "andresziemecki" # set git username
git config --global user.email "andresziemecki@gmail.com" # set email address
```

## Generating new ssh keys  to the ssh-agent from your new laptot

``` bash
ssh-keygen -t ed25519 -C "andresziemecki@gmail.com" # follow steps
eval "$(ssh-agent -s)" # checking your existing ssh -> Agent pid 59566
ssh-add ~/.ssh/id_ed25519 # Add your SSH private key to the ssh-agent
```

## Add the SSH key to your account on GitHub.

``` bash
cat ~/.ssh/id_ed25519.pub # copy the ENTIRE output to your clipboard
```

1. Sign in to github.com
2. Select your horrible face
3. Go to settings
4. Go to SSH and GCP keys
5. Select New SSH key
6. Add title and past the content

Done!



