# CMPE283 : Virtualization 
# Assignment 2:  Instrumentation via hypercall
#### 1. For each member in your team, provide 1 paragraph detailing what parts of the lab that member  implemented / researched. (You may skip this question if you are doing the lab by yourself).
- *Sirisha Polisetty(016012477)*
- *Jayanth Vishal Reddy Godi (016720080)*
#### 2. Describe in detail the steps you used to complete the assignment. Consider your reader to be someone  skilled in software development but otherwise unfamiliar with the assignment. Good answers to this  question will be recipes that someone can follow to reproduce your development steps. Note: I may decide to follow these instructions for random assignments, so you should make sure  they are accurate.

### Step 1 
- Created a VM on gcloud using the insturctions that are required for creating a virtualization machine with virtualization capabilities enabled.
- use cloud shell commmand to get the details about the account from google compute engine
- add additional details to the cloud shell command to launch instance using instructions provided.
- generate ssh key on your local machine if it not exits `ssh-keygen -t ed25519`
- Final cloud shell command with all the vm capabilitis with your ssh keys in metadata.
```
gcloud compute instances create cmpe283-assignment1 --project=valued-network-366918 --zone=us-central1-a --machine-type=n2-standard-8 --network-interface=network-tier=PREMIUM,subnet=default --metadata=ssh-keys=jayanthvishalreddy:ssh-ed25519\ AAAAC3NzaC1lZDI1NTE5AAAAIHsTFWuRw6DNxrrQgBiIx9TSgrOtdVNEoO1aWPfbHnfs\ jayanthvishalreddy@Jayanths-MacBook-Air-2.local$'\n'siri:ssh-ed25519\ AAAAC3NzaC1lZDI1NTE5AAAAICMdhjaZM4SHxu6BC7LYeX6r6yL48fbF5D\+MFwMU4w5j\ sirishacyd@gmail.com --maintenance-policy=MIGRATE --provisioning-model=STANDARD --service-account=1044074668714-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --create-disk=auto-delete=yes,boot=yes,device-name=cmpe283-assignment1,image=projects/ubuntu-os-cloud/global/images/ubuntu-2204-jammy-v20221018,mode=rw,size=100,type=projects/valued-network-366918/zones/us-central1-a/diskTypes/pd-balanced --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any --min-cpu-platform "Intel Cascade Lake" --enable-nested-virtualization
```
![](screenshots/instance_launched.png)
- Launched Instance with the SSH Keys Metadata added.

![](screenshots/ssh_keys.png)

- We can Login to the launched instance using two methods
    - ssh connect from the google compute engine [instances](https://console.cloud.google.com/compute/instances) page. Connected instance through SSH, launched on a web browser.
    ![](screenshots/3.connected_instance.png)
    - ssh connect to the instance where the private key exist for the public key that has been added for your users.
    ![](screenshots/ssh_login_siri.png)
    ![](screenshots/ssh_login_jayanth.png)

### Step 2 
- Installed required dependencies to perform the assignment that loads a new module into kernel and Launch a New VM on Kernel we are building.
```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install vim gcc make linux-headers-$(uname -r)
sudo apt-get install git fakeroot build-essential ncurses-dev xz-utils libssl-dev bc flex libelf-dev bison
sudo apt update && sudo apt install qemu-kvm -y
sudo apt-get install cloud-image-utils
```
![](screenshots/install_dependencies.png)

### Step 3

