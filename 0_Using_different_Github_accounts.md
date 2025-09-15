# Set up your Mac to both handle ITU enterprise and personal GitHub accounts

Some classes at ITU require you to use your university enterprise account or your own personal account. I have made this guide to make that workflow as smooth as possible during a busy student life.
This guide will work wether you are already logged into your enterprise account on `github.itu.dk` or whether you have just installed git. If you don't have git installed, go ahead and do that first.\
The outcome will be, that you have set up two directories on your computer, where we hardcode which credentials you will be using. This way you will always use the right account. There will be a lot of terminal interaction during this setup, but once it is done, it will all work automatically when you're working inside the correct directories.

## Moderate your `.gitconfig`

From here on out, we will be working with this folder setup:

```
Users/your-username/Documents/GitHub/
    ├── ITU/
    └── personal/
```

Your desired directory path might look different from mine, but the main requirement is, that the paths of these two directories, `ITU` and `personal`, both have a path that starts from the root directory (the full path name).

Start you terminal. Open your .gitconfig by typing `nano ~/.gitconfig`. Inside of this file you should see something like this:

```zsh
[user]
    name = ituid
    email = ituid@itu.dk
```

These are the current global user credentials that are used for every git action at this point. Delete these lines and add the following:

```zsh
[includeIf "gitdir:/Users/your-username/Documents/GitHub/ITU/**"]
    path = ~/.gitconfig-itu

[includeIf "gitdir:/Users/your-username/Documents/GitHub/personal/**"]
    path = ~/.gitconfig-personal

```

Because you can customize the directory paths, your ITU and personal directories can be located in different places and not in the same folder. But I like this simple setup. You save and close a file in the terminal by clicking `^X` and then `Y`.

Now we need to create the `.gitconfig-itu` and `.gitconfig-personal`. For simplicity keep these in the same place as the .gitconfig source file. When you open it, the terminal will show you the path at the top. It will typically be your home directory, which you can access with the command `cd ~`.

Go to the directory and create the files by typing first `touch .gitconfig-itu` and then `touch .gitconfig-personal`. Then open first the ITU file and add the lines

```zsh
[user]
    name = ituid
    email = ituid@itu.dk
```

And now you will do the same for the personal config file:

```zsh
[user]
    name = username
    email = address@gmail.com
```

Make sure this is the actual usernames of the accounts. Save this and close the file.

## Authenticate both GitHub accounts

Start by erasing current authentifications related to both domains.

```zsh
printf "protocol=https\nhost=github.com\n" | git credential-osxkeychain erase
printf "protocol=https\nhost=github.itu.dk\n" | git credential-osxkeychain erase
```

If you install the GitHub CLI (`brew install gh`), you can log in like this:

```
gh auth login
```

When it asks you `Where do you use GitHub?`, select `Other`. Enter `github.itu.dk`. Choose your preferred procotol for openrations. Either are fine, I typically use HTTPS. Follow the rest of the steps. I recommend authenticating via web browser and you should be all set for the ITU account!

Enter `gh auth login` again in the terminal and choose `GitHub.com` and follow the same steps.

You can test that both accounts receive commits from the correct account, by created a test repo on each account and cloning it into `Users/your-username/Documents/GitHub/ITU` and `Users/your-username/Documents/GitHub/personal` respectively. You should then be able to stage a commit and push it to the repo.

## Shortfalls

This guide assumes that you will only be creating git repos inside the two directories we just set up. This is fine for most ITU students. Creating repos outside of these folders might be a bit difficult now, and there are methods to alter manually between credentials by making your own custom terminal prompts, but that is outside the scope of this guide.
