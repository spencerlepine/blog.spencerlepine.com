---
title: Creating Custom Git Commands
description: Creating custom Git commands to help automate git workflow. # Dev.to
slug: creating-custom-git-commands
tags: [Git, Scripts, Terminal, Commands, GitHub] # Docusaurus
authors: [spencerlepine]
date: 2021-08-15T12:00
draft: true
---

Tired of juggling multiple commands to set up a new GitHub project? This guide introduces a clever scripting solution! We'll create a custom command that automates cloning a
repository, navigating to the directory, installing dependencies, and opening the project in VSCode - all in one go!

<!-- truncate -->

![Blog Post Thumbnail](./thumbnail.jpg)

Every time I clone a repository from GitHub, I always run the same set of commands. This is prone to typos and simply inconvenient. There is a simple solution of combining each
step into a single command that automatically runs everything for us.

In this example, I need to clone a GitHub repository, move into the new directory, and then open the project in VSCode.

Instead of multiple commands:

```sh
  git clone https://github.com/spencerlepine/readme-crawler
  cd readme-crawler
  code .
```

It would great to run one command:

```sh
	clone https://github.com/spencerlepine/readme-crawler
```

To achieve this, we can create a script in the `~/bin` directory. Make sure this path matches up with your configuration for the terminal (e.g. `PATH=$PATH:$HOME/bin`).

Let’s create a custom script to combine the git commands.

```sh
  #!/bin/bash

  ((!$#)) && echo missing git URL argument! && exit 1

  git clone $1
  basename=$(basename $1)
  reponame=${basename%.*}
  cd $reponame
  npm install
  code .
```

Use this script or create your own, and follow these steps to set up the custom command:

- Navigate to usr/local/bin -> `cd ~/../../usr/local/bin`
- Run `vim clone`
  - _Paste the script_
- Save the file:
  - \*press ‘ESC’
  - \*press ‘SHIFT’ + ‘:’
  - \*type ‘wq’ + ENTER
- Create an executable
  - `chmod +x clone`
- Run the command!
  - `clone https://github.com/spencerlepine/manyshiba-bot.git`

Viola! This script will accept one command line argument of the destination repo URL. It will automatically open the new project in VSCode in one command.

Follow my journey and connect with me here:

- LinkedIn: [/in/spencerlepine](https://www.linkedin.com/in/spencerlepine/)
- Email: [spencer.sayhello@gmail.com](mailto:spencer.sayhello@gmail.com)
- Portfolio: [spencerlepine.com](https://spencerlepine.com)
- GitHub: [@spencerlepine](https://github.com/spencerlepine)
- Twitter: [@spencerlepine](https://twitter.com/spencerlepine)
