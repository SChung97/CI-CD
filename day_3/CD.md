# CD(e) - continuous delivery/deployment

- CI pipeline must be completed in order to implement CD
- we now want to deliver the new code to an AWS EC2 instance
- app doesn't need to be running within the instance, but must have app dependencies ready
- we want jenkins to SSH into the target AWS instance, copy the new code from CI pipeline and run the new code (running the new code will be deployment)

- create a new EC2 instance using the app image, and standard app security group rules
- make sure to add your key pair to allow Jenkins to log in

# Job 3 - Deploy to AWS

- continuous delivery (will still have to manually deploy):
- create a new item and name it eg. 'steph-job3-cd-test'
- copy item from job 2 (merge job)
- change the description eg. 'delivery of new code to prod instance'
- keep discard builds and all github settings the same
- under build triggers, change projects to watch to the second job eg. 'steph-new-ci-merge'
- leave build environment settings as is (but should also work without them)
- remove git publisher settings, under post build actions section

- under build environment, tick SSH agent
- add credentials for aws private key
- under build steps, select execute shell to add commands to run

```
ls
cd nodejs20-se-test-app-2025
 ls
 rsync -avz -e "ssh -o StrictHostKeyChecking=no" app ubuntu@52.215.93.8:/home/ubuntu

 ssh -o "StrictHostKeyChecking=no" ubuntu@52.215.93.8 <<EOF
 ls
 cd app
 ls
 EOF
```

- rsync will sync up the code on the agent node to the EC2 instance - more efficient and better for automation
- copy and paste the public ip address of the instance
- also checks that we can ssh into the instance

- save the item
- should trigger once a merge has been applied (manually build first to check it works)

- to implement continuous deployment:

- add code to execute shell:

```
npm install
pm2 kill
pm2 start app.js
```

- 