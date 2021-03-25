---
layout: post
title: Set GitHub SSH Key For Password-free Push
description: I need to do this on every new machine. So I keep a note for my quick reference.
permalink: /set-github-ssh-key/
categories: [blog]
tags: [GitHub, SSH, Key, auth]
date: 2021-03-25 12:35:19
---

# References

Here are the links for the detailed configurations and so on.

-   [Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
-   [git 仓库从 http 链接转为 ssh](https://blog.csdn.net/xl_1851252/article/details/81274721)

# Steps

1.  `$ ssh-keygen -t ed25519 -C "your_email@example.com"`
    
    You will be asked about the secure passphrase. I prefer letting it empty. Otherwise you need to enter this password every time you `git push`.

2.  `$ eval "$(ssh-agent -s)"`: Test whether the SSH agent work or not.
3.  `$ ssh-add ~/.ssh/id_ed25519`
4.  `cat ~/.ssh/id_ed25519.pub`: copy the output of this command
5.  Go to the GitHub personal setting -> "SSH and GPG keys" on the left panel -> "New SSH key" -> Paste the above output to the input.
6.  Test: `ssh -T git@github.com`.
    
    Output:
    
    ```shell
    The authenticity of host 'github.com (140.82.112.4)' can't be established.
    RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
    Are you sure you want to continue connecting (yes/no)? yes
    Warning: Permanently added 'github.com,140.82.112.4' (RSA) to the list of known hosts.
    Hi <your_username>! You've successfully authenticated, but GitHub does not provide shell access.
    ```

7.  Done.

# Change the Local Repo's Remote Address

Assume your project is `awesome-project`, then edit `url` in `awesome-project/.git/config`.

Before: `url = https://<your_github_username>@github.com/<your_github_username>/awesome-project.git`

After: `url = git@github.com:<your_github_username>/awesome-project.git`

# End

Now you don't need to enter password again when `git push` or `git pull`.
