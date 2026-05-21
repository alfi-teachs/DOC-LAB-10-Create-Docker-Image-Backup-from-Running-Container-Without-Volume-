When a volume is not attached, all files and configuration stay inside the container.
You can create a backup of that container using docker commit.

# Step 1: Run Nginx Container
```bash
docker run -d -p 1010:80 --name=cont1 nginx
```
Check running containers:
```bash
docker ps
```
# Step 2: Enter Inside Container
```bash
docker exec -it cont1 /bin/bash
```
# Step 3: Go to Nginx HTML Directory
```bash 
cd /usr/share/nginx/html
```
Check files:
```bash
ls
```
# Step 4: Install Vim Editor

Update packages:
```bash
apt update
```
Install vim:
```bash
apt install vim -y
```
# Step 5: Remove Default Files
```bash
rm -rf *
```
# Step 6: Create HTML Web Page
```bash
vim index.html
```
Press i to enter insert mode.
Paste HTML content:
```bash
<h1>Docker Backup Image Demo</h1>
<h2>Container Data Saved Inside Image</h2>
```
Save and exit:

ESC + :wq
# Step 7: Create Sample Files
```bash
touch file{1..20}
```
Check files:
```bash
ls
```
# Step 8: Exit Container
```bash
exit
```
# Step 9: Create Image Backup from Running Container
```bash
docker commit cont1 my-new-image
```

This creates a new image with all files and configuration stored inside the container.

# Step 10: Verify Image Created
```bash
docker images
```
You will see:

my-new-image
# Step 11: Launch New Container Using Backup Image
```bash
docker run -d -p 1050:80 --name cont3 my-new-image
```
# Step 12: Verify Backup Data

Enter new container:
```bash
docker exec -it cont3 /bin/bash
```
Go to HTML directory:
```bash
cd /usr/share/nginx/html
```
Check files:
```bash
ls
```
You will see:
```bash
index.html
```
file1 to file20

This proves the container backup image contains all data.

# Step 13: Test Website in Browser

Open browser:
```bash
http://localhost:1050
```
You will see your HTML webpage running from the backup image.

# Important Understanding
docker commit saves:
Installed packages
Files

Configuration changes
docker commit does NOT save:
Attached external volumes
When to Use Docker Commit

# Use it when:
Volume is not attached
You want quick backup of container state
Testing or lab practice
Creating custom reusable images

For production environments, Dockerfile + Volumes is the better approach.
