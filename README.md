<em>GADS-2020-cloud-projects-translation </em> <br/>
***LAB 1: APP DEV-SETTING UP A DEVELOPMENT ENVIROMENT***

**Objectives**
 * In this lab, you will learn how to perform the following tasks:
 * Provision a Google Compute Engine instance.
 * Connect to the instance using SSH.

**Steps: Creating a Compute Engine Virtual Machine Instance**
  * In the Cloud Platform Console, on the Navigation menu, click Compute Engine.
  * On the VM Instances page, click Create.
  * On the Create an instance page, for Name type
     dev-instance, 
  * select us-central1 for region and us-central1-a for the zone.
  
 ** 1.  Install software on the VM instance**
  * In the SSH session, to update the Debian package list, execute the following command:
      sudo apt-get update

  * To install Git, execute the following command:
      sudo apt-get install git

  * If prompted, press Enter.
    To download the Node.js setup script, execute the following command:
      curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -

  * To install npm and Node.js, execute the following command:
      sudo apt install nodejs

**2.  Configure the VM to Run Application Software**
In this section, you will verify the software installation and run some sample codes.

  * To check the version of Node.js, execute the following command:
        node -v
    You should see the Node.js version number for version 6.

  * To clone the class repository, execute the following command:
        git clone https://github.com/GoogleCloudPlatform/training-data-analyst

  * To change the working directory, execute the following command:
        cd ~/training-data-analyst/courses/developingapps/nodejs/devenv/

  * To run a simple web server, execute the following command:
        sudo node server/app.js

Return to the Cloud Console VM instances list, and click on the External IP address for the dev-instance.
You should see a Hello GCP dev! message from Node.js.
Return to the SSH window, and stop the application by pressing Ctrl+C.

  * To install the Node.js library for Compute Engine, execute the following command:
        npm install

  * To run a simple Node.js application that lists Compute Engine instances, execute the following command:
        node list-gce-instances.js

    Many details about your machine should appear in the terminal window.

  ***END OF LAB***


***LAB 2: Google Cloud Fundamentals: Getting Started with Compute Engine***
**Objectives**
In this lab, you will learn how to perform the following tasks:
  * Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.
  * Create a Compute Engine virtual machine using the gcloud command-line interface.
  * Connect between the two instances.

***Steps: Sign in to the Google Cloud Platform (GCP) Console***

**1. Create a virtual machine using the GCP Console
        gcloud compute instances create "my-vm-1" --machine-type "n1-standard-1" 
        --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --subnet "default" --tags http

**2. Create a virtual machine using the gcloud command line
        gcloud compute zones list | grep us-central1
        gcloud compute instances create "my-vm-2" --machine-type "n1-standard-1"
         --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --subnet "default"

 **3. Connect between VM instances
 
      * Use the ping command to confirm that my-vm-2 can reach my-vm-1 over the network:
             ping my-vm-1

      * Use the ssh command to open a command prompt on my-vm-1:
            ssh my-vm-1

        If you are prompted about whether you want to continue connecting to a host with unknown authenticity, 
        enter yes to confirm that you do.

      * At the command prompt on my-vm-1, install the Nginx web server:
            sudo apt-get install nginx-light -y

      * Use the nano text editor to add a custom message to the home page of the web server:
            sudo nano /var/www/html/index.nginx-debian.html

      * Confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:
            curl http://localhost/

      *To confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:
            curl http://my-vm-1/

Congratulations!

***END OF LAB***


**LAB 3: Google Cloud Fundamentals: Getting Started with GKE

**Objectives

In this lab, you learn how to perform the following tasks:
    * Provision a Kubernetes cluster using Kubernetes Engine.
    * Deploy and manage Docker containers using kubectl.

**Steps: Sign in to the Google Cloud Platform (GCP) Console

    1. Confirm that needed APIs are enabled
        Make a note of the name of your GCP project. This value is shown in the top bar of the Google Cloud Platform Console. It will be of the form qwiklabs-gcp- followed by hexadecimal numbers.

    2. In the GCP Console, on the Navigation menu (Navigation menu), click APIs & Services.Scroll down in the list of enabled APIs, and confirm that both of these APIs are enabled:
        Kubernetes Engine API
        Container Registry API

     3. Start a Kubernetes Engine cluster
        Place the zone that Qwiklabs assigned you to into an environment variable called MY_ZONE. At the Cloud Shell prompt, type this partial command:
            export MY_ZONE=
        followed by the zone that Qwiklabs assigned to you. Your complete command will look similar to this:
    
            export MY_ZONE=us-central1-a

    4. Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster webfrontend and configure it to run 2 nodes:

            gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2

    5. After the cluster is created, check your installed version of Kubernetes using the kubectl version command:

            kubectl version

    6. Run and deploy a container
       From your Cloud Shell prompt, launch a single instance of the nginx container. (Nginx is a popular web server.)

            kubectl create deploy nginx --image=nginx:1.17.10

    7. View the pod running the nginx container:

            kubectl get pods

    8. Expose the nginx container to the Internet:

            kubectl expose deployment nginx --port 80 --type LoadBalancer

    9. View the new service:

            kubectl get services

    10. Scale up the number of pods running on your service:

            kubectl scale deployment nginx --replicas 3

    11. Confirm that Kubernetes has updated the number of pods:

            kubectl get pods


Congratulations!

***END OF LAB***
