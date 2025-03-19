---
title: 'Multiple SSH keys for different accounts on Github or Gitlab'
date: '2025-03-14'
description: 'Step by step to config multiple SSH keys'
---

# Create SSH keys with different names

```
ssh-keygen -t rsa -C "your_name@home_email.com"
ssh-keygen -t rsa -C "your_name@company_email.com"
```

- When you see this message

```
Generating public/private rsa key pair.
Enter file in which to save the key (/home/user_name/.ssh/id_rsa):
```

- Enter unique name, for example:

```
id_rsa_personal
// At this case. we should type dir /home/user_name/.ssh/id_rsa_personal
id_rsa_company
// At this case like this
```

# After all steps you can check that all keys were created

```
$ ls ~/.ssh
```

- You should see a similar files list:

```
id_rsa_home  id_rsa_company  id_rsa_home.pub  id_rsa_company.pub
```

# Now you need a config file for organize

```
$ cd ~/.ssh/
$ touch config
$ nano config
```

# Add into config file

```
# Note: This is my config. You can change it by you require

# GITLAB

Host company.gitlab.com
HostName company.gitlab.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa_company

# GITHUB

Host personal.github.com
HostName personal.github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa_home
```

# Next you'll delete cached keys

```
ssh-add -D
```

- If you see a message: Could not open a connection to your authentication agent.
- Then enter:

```
eval `ssh-agent -s`
```

- You can check that your keys were Added

```
ssh-add -l
```

If you haven't any entries then you should add your keys

```
ssh-add ~/.ssh/id_rsa_personal
ssh-add ~/.ssh/id_rsa_company
```

- After all you should add keys into github/gitlab
