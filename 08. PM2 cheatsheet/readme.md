If you lost your services when restarting the Linux machine use the below 3 commands all pm2 services will back.
```
pm2 startup         # Detect init system, generate and configure pm2 boot on startup
pm2 save            # Save current process list
pm2 resurrect       # Restore previously saved processes
```
How to create service of a pm2 

```
pm2 start "controllers/index.js" --name "Give a unique name that will appear in pm2 list"
```

How to list all the running services with pm2
```
pm2 list
```

How to check a pm2 service is configured
```
pm2 show 0
```
Replace 0 with the serial number you want to check
