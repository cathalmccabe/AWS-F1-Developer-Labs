<table style="width:100%">
  <tr>
    <th width="100%" colspan="5"><h2>SDAccel AWS F1 Developer Labs</h2></th>
  </tr>
  <tr>
    <td width="20%" align="center"><a href="README.md">Introduction</a></td>
    <td width="20%" align="center"><b>1. Connecting to your F1 instance</b></td> 
    <td width="20%" align="center"><a href="2_HELLOWORLD.md">2. Running Helloworld</a></td>
    <td width="20%" align="center"><a href="3_IDCT.md">3. Developing F1 applications</a></td>
    <td width="20%" align="center"><a href="4_WRAP_UP.md">4. Wrapping-up</a></td>
  </tr>
</table>

---------------------------------------
### Setting-up an F1 instance

In this module you will start a pre-configured EC2 F1 instance and connect to it using a remote desktop client. 

#### Prerequisites

In order to run the SDAccel AWS F1 Developer Labs, you will need the following:

1. An AWS account
If you do not already have an Amazon Web Services (AWS) account, create one here: [https://aws.amazon.com/](https://aws.amazon.com)

1. Access to AWS F1 instances
By default, AWS users do not have access to F1 instances. You need to request and be granted access to F1 instances before you can start using these instance. 

<details>
<summary><strong>Step-by-step instructions</strong> <i>(expand for details)</i></summary><p>

* Open the Service Limit Increase form: [http://aws.amazon.com/contact-us/ec2-request](http://aws.amazon.com/contact-us/ec2-request)
* Make sure your account name is correct
* Submit a 'Service Limit Increase' for 'EC2 Instances'
* Select the region where you want to access F1 instances: US East (N.Virginia), US West (Oregon) or EU (Ireland)
* Select 'f1.2xlarge' as the primary instance type
* Set the 'New limit value' to 1 or more
* Fill the rest of the form as appropriate and click 'Submit'

Requests are typically processed by AWS in 24 to 48 hours.
<p></details><br>


#### Starting an EC2 F1 instance with the SDAccel AWS F1 Developer Labs AMI
1. Navigate to the AWS EC2 dashboard: [https://console.aws.amazon.com/ec2](https://console.aws.amazon.com/ec2)
1. In the top right corner, select a region with F1 instances: US East (N.Virginia), US West (Oregon) or EU (Ireland) 
1. Click 'Launch Instance'

#### Choose an Amazon Machine Image (AMI)
1. Click 'AWS Marketplace' (on the left pane, second item under Quick Start)
1. Search for 'SDAccel'
1. Select the 'SDAccel AWS F1 Developer Labs AMI'
1. This brings up a pop-up screen showing rates for each instance type
1. Click 'Continue'

#### Choose an Instance Type
1. Select a 'f1.2xlarge' instance
1. Click 'Next: Configure Instance Details'. **Do not click 'Review and Launch'**

#### Configure Instance
1. At the bottom of the page, open the 'Advanced Details' section and add the following user data as text:
```bash
#!/bin/bash
echo “centos:sdaccel_labs” | sudo chpasswd
```
1. Click 'Review and Launch'

#### Review and Launch
1. Click 'Launch'
1. Select an existing key pair or create a new key pair
1. Click the check box at the bottom of the dialog
1. Click 'Launch Instances'

#### Launch Status
1. A message confirms that your instance is being launched
1. Click the instance name to display it in the instance view
1. Copy the IPv4 Public IP address of the instance. **You will need it to connect to your instance.**

When the status of the newly launched instance switches to green (Running), you are ready to connect to it.
    ![Start](./images/setup_lab/start1.png?raw=true)

    - Allow about 10 seconds for the instance to get in the 'running' state. 
    - If needed, click the **Refresh** icon (![Refresh](./images/setup_lab/refresh2.png?raw=true)) in the top-right corner of the EC2 Console to update the instance status information.


#### Connect to your instance using a remote desktop client

The instance you just started is preconfigured with remote desktop protocol (RDP) services.

1. From your local machine, start a remote desktop protocol client
    - **IMPORTANT**: Before connecting, set your remote desktop client to use **24-bit for color depth**
      - Windows client: In the bottom-left corner of connection prompt, click Options, then select the Display tab and set Colors to True Colors (24 bit)
    - On Windows: press the Windows key and type "remote desktop".
      - You should see the "Remote Desktop Connection" in the list of programs.
      - Alternatively you can also simply type `mstsc.exe` in the Windows run prompt.
    - On Linux: RDP clients such a Remmina or Vinagre are suitable.
    - On macOS: use the Microsoft Remote Desktop v8.0.43 (that version offers color depth settings) from the Mac App Store.

1. In the RDP client, enter the **IPv4 Public IP** of your instance.

1. Click **Connect**. This should bring up a message about connection certificates. 

1. Click **Yes** to dismiss the message. The Remote Desktop Connection window opens with a login prompt.

1. Login with the following credentials:
    - User: **centos**
    - Password: **sdaccel_labs**
   
    ![Remote](./images/setup_lab/remote1.png?raw=true)
   
1. Click **Ok**.

You should now be connected to the remote F1 instance running Centos 7.

#### Open the lab instructions on the remote F1 instance

1. In the remote instance, double click on the **Chromium** icon.
    - It opens the browser and loads the lab instructions.
    
    _Note: if a "keyring" popup comes up, click Cancel._

1. Continue following the lab instructions from within the remote instance and the Chromium browser.
    - We suggest you perform all your copy-paste from the instructions to the shell within the RDP session to avoid issues.

#### Configure the Xilinx SDAccel environment and load the workshop files

1. Open a new terminal by right-clicking anywhere in the Desktop area and selecting **Open Terminal**.

1. In the terminal, `git clone` the SDAccel-AWS-F1-Developer repository to download the files for the Xilinx Developer Lab.

    ```bash  
    cd /home/centos
    git clone https://github.com/Xilinx/SDAccel-AWS-F1-Developer-Labs.git
    ```

1. Source the SDAccel environment. 

    ```bash  
    cd ~/aws-fpga
    source sdaccel_setup.sh
    ```

    *Note: the sdaccel_setup.sh script might generate warning messages, but these can be safely ignored.*


You instance is now configured to run the SDAccel Developer labs on AWS F1. The next step is to run the "helloworld" example to confirm everything works correctly.

---------------------------------------

<p align="center"><b>
Start the next module: <a href="2_HELLOWORLD.md">2. Running Helloworld</a>
</b></p>
