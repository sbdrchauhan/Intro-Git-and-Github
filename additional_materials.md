## What is Git Bash?
Git Bash for Windows is a package that includes both *Git* and *Bash*.

Git is an open-source version control system for tracking source code changes when developing software. It keeps a commit history that allows you to revert to a stable state in case you make errors in your code. Git also enables multiple developers to collaborate on the same code base.

Bash is a Unix command-line shell. The name is an acronym for *Bourne-Again Shell*. It comes with useful Unix commands like **cat, ssh, SCP, etc.**, which are not usually found on Windows.
## Download GitBash in windows 64 bit
1. Go to the [Git download page](https://git-scm.com/downloads?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-wwwcourseraorg-SkillsNetworkCoursesIBMDeveloperSkillsNetworkCD0101ENSkillsNetwork20336975-2021-01-01)
2. Follow the default
3. Select Use the OpenSSL library. Click Next.
4. Configure your line ending conversions for Windows by selecting the default option, Checkout Windows-style, commit Unix-style line endings. Click Next.
5. Configure your terminal emulator to use with Git Bash by selecting the default option, Use MinTTY(the default terminal of MSYS2). Click Next.
6. Configure the default behavior for a git pull by selecting Default (fast-forward or merge). Click Next.
7. Select any additional options you want to install. (The default option is sufficient to use Git Bash successfully.) Click Next.
8. You can enable experimental options if you choose to. By enabling these options, you will be able to try newer features that are still being developed. However, you do not have to select any experimental options to use Git Bash. Click Install to complete the installation with the options you have chosen. The installation runs and when complete, a Completing the Git Setup Wizard window opens.
9. The Git Bash terminal opens. You are now able to enter Git and Bash commands.

## SSH key
An SSH key is an access credential in the SSH protocol. Its function is similar to that of user names and passwords, but the keys are primarily used for automated processes.

## Generating SSH key
To generate an SSH key, complete the following steps:
1. Launch a terminal. If you are using Windows, launch Git Bash.
2. Type the following command in your terminal, replacing <your email address> with the email address that is linked to your Github account. When you have typed the command, press Enter.
  ssh-keygen -t rsa -b 4096 -C "<your email address>"
    A new SSH key is generated.
3. You will be prompted to enter a directory to save the key. You can simply press Enter to accept the default location, which is an .ssh folder in the home directory. This means you will be able to locate the key in ~/.ssh/id_rsa.
4. You will be prompted to choose a passphrase. You also have the option not to create a passphrase. To skip the passphrase, press Enter twice to confirm that the passphrase is empty.
5. Optional: To navigate to the .ssh directory, and check the contents of the directory, run the following commands in the terminal:

    cd ~/.ssh

    and then,

    ls

    When you list the contents of the .ssh directory, you should see id_rsa and id_rsa.pub in the list of contents, where id_rsa is the private version of your key and id_rsa.pub is the public version of your key.
6. You now need to add the SSH key to the ssh-agent, which helps with the authentication process. To start the ssh-agent, run the following command in the terminal:

    eval "$(ssh-agent -s)"
7. To add the key to the agent, run the following command in the terminal:

    ssh-add ~/.ssh/id_rsa

To add SSH key to GitHub: follow the first step in readme.md
