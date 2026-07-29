# h5 Version Control

## Summary
### Chacon and Straub 2014: 

- Git is a version control system used to manage changes in projects.
- It works locally, meaning commits and history are always on your own machine.

### git add . && git commit; git pull && git push

- The purpose of git add . is to add file contents to the index. (Git)
- && runs the next command only if the previous one succeeded. (GeeksforGeeks 2020)
- The purpose of git commit is to save the changes to the repository. (Git)
- ; is a command separator. (GeeksforGeeks 2020)
- The purpose of git pull is to fetch new commits and merge them into the current branch. (Git)
- The purpose of git push is to send locally made commits to the remote repository. (GitHub Docs 2025)

  ### Commits

  - Repo development: creating the basic structure, a hello world Salt module, and finally adding small improvements. (Tero Karvinen 2024)

## Online

I created a new repository on GitHub called snow-project.

<img width="634" height="254" alt="image" src="https://github.com/user-attachments/assets/6a0f5f7e-e325-4ce2-a500-c2f4069697a6" />


## Dolly

I created a new SSH key using the command ssh-keygen. I checked and copied the public key using the command cat ~/.ssh/id*.pub, after which I added it to GitHub.
I tested the connection to GitHub using the command ssh -T git@github.com.

<img width="632" height="26" alt="image" src="https://github.com/user-attachments/assets/4f453484-ec3f-4710-acc3-e3e43f1969b8" />

Next, I created a folder called project using the command mkdir project and moved into it with the command cd ~/project. I ran the command git clone git@github.com:satuharjula/snow-project.git snow-project-ssh. 

<img width="618" height="101" alt="image" src="https://github.com/user-attachments/assets/e253c27c-ff0b-4e92-8cd5-fdf3bba151ef" />

I moved into the directory with cd snow-project-ssh and entered the command git remote -v to see that the repo had been cloned.

<img width="614" height="36" alt="image" src="https://github.com/user-attachments/assets/34273cac-adfe-4f73-bdb1-9c740ee7b1a5" />

Next, I moved into the SSH-cloned folder using the command cd ~/project/snow-project-ssh and opened README.md with the command nano README.md.

I added content to the README.md file:

<img width="631" height="101" alt="image" src="https://github.com/user-attachments/assets/69059602-5a4b-48ef-b3bc-2fa736f97309" />

I checked the change with the command git status.

<img width="635" height="148" alt="image" src="https://github.com/user-attachments/assets/f7c9bd60-2090-4e3b-8df0-b744b20e6835" />

I made a commit with the commands git add README.md and git commit -m "Test change".

<img width="628" height="31" alt="image" src="https://github.com/user-attachments/assets/19daa1ca-a215-44da-9896-bc0f9a0727b1" />

I pushed the change to Git with the command git push origin main.

<img width="624" height="122" alt="image" src="https://github.com/user-attachments/assets/80eed779-68d7-4d35-9898-b4076081d70e" />

Finally, I checked that the change appeared on GitHub. (Git)

<img width="506" height="394" alt="image" src="https://github.com/user-attachments/assets/d2aeb17c-e9e7-40b2-aa27-7645b64eda31" />


## Doh!

I moved to edit the README.md file with the command nano README.md and added some clutter (test text).

<img width="602" height="116" alt="image" src="https://github.com/user-attachments/assets/f97c8ef5-34e4-417f-8c83-eaa24f09e6ee" />

I entered the command git status to check that Git noticed the change.

<img width="632" height="147" alt="image" src="https://github.com/user-attachments/assets/52abedd6-ca9b-40a7-8c24-4af4d627961b" />

Next, I entered the command git reset --hard, which restores the files to the state of the most recent commit.

After this, I entered the command git status to see that the change had disappeared.

<img width="632" height="107" alt="image" src="https://github.com/user-attachments/assets/6fd85aa5-7c5d-48ad-b4c1-b68a836873d5" />

Finally, I checked with the command cat README.md that my text had disappeared.

<img width="603" height="76" alt="image" src="https://github.com/user-attachments/assets/6ea6ca5a-9fcf-4bcd-81bd-a808c211cdc9" />

## Log

I examined my log with the command git log. The command shows the author's name and email address, the time the commit was made, and a message that briefly describes what was changed.

<img width="991" height="221" alt="image" src="https://github.com/user-attachments/assets/51f400d3-33b8-4615-970d-b29c110e3dcf" />

## Salted shard

I moved into the repo with the command cd ~/project/snow-project and created a new salt directory with the command mkdir -p salt, and created a top.sls file inside the directory with the command nano salt/top.sls.

I added the following content to top.sls:

<img width="532" height="187" alt="image" src="https://github.com/user-attachments/assets/2671a145-9cd4-4896-8fb9-2235175d004a" />

I created a test.sls file inside the salt directory with the command nano salt/test.sls.

I added the following content to test.sls:

<img width="577" height="137" alt="image" src="https://github.com/user-attachments/assets/2b431b16-c178-4937-90ac-05deb3319e7a" />

I ran the Salt states with the command sudo salt-call --local --file-root salt/ state.apply.

<img width="623" height="266" alt="image" src="https://github.com/user-attachments/assets/e05f2f76-2a8b-489f-a97e-1291c45d07d3" />

Finally, I added the Salt files to version control and pushed them to GitHub with the following commands:

<img width="643" height="223" alt="image" src="https://github.com/user-attachments/assets/20721460-3ddf-4921-a25b-f72c334a0be6" />

I checked that the files appeared in the snow-project on GitHub:

<img width="418" height="283" alt="image" src="https://github.com/user-attachments/assets/0d64006d-3172-4126-b1da-9ff48b7b840f" />

<img width="443" height="271" alt="image" src="https://github.com/user-attachments/assets/96c15b8c-9000-4094-a72b-ffbf21335cf6" />


## Sources:

GeeksforGeeks. 14 October 2020. Difference Between && and ; chaining operators in Linux. URL: https://www.geeksforgeeks.org/linux-unix/difference-between-chaining-operators-in-linux/. Accessed: 23 November 2025.

GitHub Docs. 2025. Pushing commits to a remote repository. URL: https://docs.github.com/en/get-started/using-git/pushing-commits-to-a-remote-repository. Accessed: 23 November 2025

Git. URL: https://git-scm.com/docs/git-add. Accessed: 23 November 2025.

GitHub. Karvinen, T. 10 April 2024. Suolax. Commits. URL: https://github.com/terokarvinen/suolax/commits/main/. Accessed: 23 November 2025. 
