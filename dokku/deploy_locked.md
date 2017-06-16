## Deploy Locked

if you push to stage and a message like the following shows up:


```
Counting objects: 4, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 355 bytes | 0 bytes/s, done.
Total 4 (delta 2), reused 0 (delta 0)
remote: pjec is currently being deployed. Exiting...
To dokku@rauluranga.com:pjec
 ! [remote rejected] master -> master (pre-receive hook declined)
error: failed to push some refs to 'dokku@rauluranga.com:pjec'
```

`remote: pjec is currently being deployed. Exiting...` 
means that for some reason your app deployment is locked.
if you need to force deployment, don't worry, just delete the following files on your server and then try to deploy again:

```
/home/dokku/app/.build.lock
/home/dokku/app/.deploy.lock
```
