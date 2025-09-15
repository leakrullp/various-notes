# Set up your Mac to both handle ITU enterprise and personal GitHub accounts

This guide will work wether you are already logged into your enterprise account on `github.itu.dk` or whether you have just installed git. If you don't have git installed, go ahead and do that first.\
The outcome will be, that you have set up two directories on your computer, where we hardcode which credentials you will be using. This way you will always use the right account. There will be a lot of terminal interaction during this setup, but once it is done, it will all work automatically when you're working inside the correct directories.

## 1) Moderate your `.gitconfig`

From here on out, we will be working with this folder setup:

```
Users/your-username/Documents/GitHub/
    ├── ITU/
    └── personal/
```

Your directory path might look different from mine, but the main requirement is, that the paths of these two directories, `ITU` and `personal`, both have a path that starts from the root directory of the machine(the full path name).\
You will be able to manually switch between the aliases when you are outside the scope of these folders, but these will be hardcoded to make sure that you are always commiting as the correct alias depending on which directory you are in.

If you want a different setup or logic in your `.gitconfig`, ChatGPT is your friend.

Open your .gitconfig from any directory by typing `nano ~/.gitconfig`. Inside of this file you should see something like this:

```zsh
[user]
    name = leape
    email = leape@itu.dk
```

These are the current global user credentials that are used for every git action at this point. Delete these lines, add the following:

```zsh
[includeIf "gitdir:/Users/your-username/Documents/GitHub/ITU/**"]
    path = ~/.gitconfig-itu

[includeIf "gitdir:/Users/your-username/Documents/GitHub/personal/**"]
    path = ~/.gitconfig-personal

```

Because you can customize the directory paths, your ITU and personal directories can be located in different places and not in the same folder. But I like this simple setup.

## 3) Authenticate both GitHub accounts

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

You can test that both accounts receive commits from the correct account, by created a test repo on each account and cloning it into `Users/your-username/Documents/GitHub/ITU` and `Users/your-username/Documents/GitHub/personal` respectively. You should then be able to stage a commit and push it to the repo

## Shortfalls

This guide assumes that you will only be creating git repos inside the two directories we just set up. This is fine for most ITU students. Creating repos outside of these folders might be a bit difficult now, and there are methods to alter manually between credentials by making your own custom terminal prompts, but that is outside the scope of this guide.
