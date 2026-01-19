automation is set up on the "control node"

- start by creating a new item and give it a name
- select freestyle project
- add a description eg. testing Jenkins
- check discard old builds - can control the maximum number of builds you want
- untick restrict where this project can be run
- can add a bash script under build steps section, click execute shell
- click build now when ready to run
- can set new jobs to run automatically run after (or even before)


- ssh needs to be set up between github and jenkins (unable to enter passwords)
- must create a web hook - alerts Jenkins of any changes

**Create a new key-pair:**
- cd into .ssh folder
- run the command: `ssh-keygen -t rsa -b 4096 -C "youremailaddress"`
- name your public key
- leave pass phrase blank - Jenkins cannot enter the pass phrase
- will create both public and private key (private key won't have an extension) - remember private key is sensitive!

- within github repo, under settings click deploy key
- Add a new key and cat public key
- copy and paste the public key within the key section, and press allow write access (will allow for automated merges)

- add the private key to Jenkins or can be done separately or when the job is built

**Create the webhook:**
- under settings, select webhook
- add webhook to the same repo containing the code, add the payload url `http://server-ip-address:8080/github-webhook/`
- disable ssl verification for now
- select only the push event to trigger the webhook

# Job 1 - source code management (scm) and build
- create a new item and give it a name eg. `steph-job1-ci-test`
- select freestyle project
- give the new item a description

- tick discard old builds, set max number to 3
- tick github project, and paste the https url of the github repo (add forward slash to the end of the url)
- untick restrict where the project can be run
- under source code management, copy and paste the SSH url - will give a wall of red text first as no credentials
- select add credentials, and then select Jenkins - will allow us to add private key

- leave global credentials (unrestricted) as is
- select SSH username with private key
- leave scope as is
- set ID eg. `tech519-steph-github-key-pair`
- can copy and paste into description and username
- leave keep username a secret unticked
- within bash terminal, cat the private key and paste it into Jenkins (will begin and end with dashes)
- select your key pair within credentials drop down (wall of red text will be removed)

- under branches to build section, change to */main (was master)
- under build environment, select provide node & npm bin/ folder to PATH
- change nodeJS version to 20
- leave the remaining settings as default

- add execute shell to build steps
```
ls
cd nodejs20-se-test-app-2025
ls
cd app
ls
npm install
npm test
```

- save the item
- run the build - created manually to test the ssh key has been correctly added

**implementing the webhook:**
- under build triggers, select github hook trigger for gitscm
- change branch specifier from */main to */dev
- save changes
- if you make a change to code, switch to dev branch `git chekout -b dev` first! make sure you push to the dev branch as well!
- merge on github by comparing pull requests
# Job 2 - testing and merge

# Job 3 - Deploy to AWS