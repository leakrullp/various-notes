# Set up your Mac to both handle ITU enterprise and personal GitHub accounts

This guide assumes that your computer is set up to use your ITU credentials to commit to the domain `github.itu.dk`.\
The outcome will be, that you have set up your systems to handle two aliases, and a directory on your computer, where we hardcode which alias you will be comitting as. This way you will always use the right account.

## 1. Create the two aliases you will be using

Open your terminal on your Mac. We are modifying the Zsh shell (the standard, unless you changed it) two respond to two new prompts; `git_itu` and `git_personal`. These will manually switch between the two account credentials.\
Go to your zshrc file by typing `nano ~/.zshrc` in the command line.
Add the following lines to your file:

```
alias git_personal='git config --global user.email {my.email@gmail.com} && git config --global user.name {leakrullp}'

alias git_itu='git config --global user.email {leape@itu.dk} && git config --global user.name {leape}'
```

## Moderate your `.gitconfig`

From here on out, we will be working with this folder setup:

```
~/Documents/GitHub/
    ├── ITU/
    └── personal/
```

If you just make sure, that somewhere on your machine has a directory named `Documents/GitHub` which then contains the at least the two directories `ITU` and `personal` you can copy and paste my exact code.\
You will be able to manually switch between the aliases when you are outside the scope of these folders, but these will be hardcoded to make sure that you are always commiting as the correct alias depending on which directory you are in.

If you want a different setup or logic in your `.gitconfig`, ChatGPT is your friend.

Open your .gitconfig from any directory by typing `nano ~/.gitconfig`. Inside of this file you should see something like this:

```zsh
[user]
    name = leape
    email = leape@itu.dk
```

These are the standard credentials that are used for every commit at this point. Below these lines, add the following:

```zsh
[includeIf "gitdir:~/Documents/GitHub/ITU/**"]
    path = ~/.gitconfig-itu

[includeIf "gitdir:~/Documents/GitHub/personal/**"]
    path = ~/.gitconfig-personal
```

Now we need to create the `.gitconfig-itu` and `.gitconfig-personal`. For simplicity keep these in the same place as the .gitconfig source file. When you open it, the terminal will show you the path at the top. It will typically be your home directory, which you can access with the command `cd ~`.

Go to the directory and create the files by typing first `touch .gitconfig-itu` and then `touch .gitconfig-personal`. Then open first the ITU file and add the lines

```zsh
[user]
    name = leape
    email = leape@itu.dk
```

And now you will do the same for the personal config file:

```zsh
[user]
    name = ...
    email = ...
```

Save this and close the file.

## Test that both directories commit as the right alias

blabla

## Test the manual switching

blabla
