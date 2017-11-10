<table style="width:100%">
  <tr>
    <th width="100%" colspan="5"><h2>SC17 Xilinx Developer Lab</h2></th>
  </tr>
  <tr>
    <td width="20%" align="center"><a href="README.md">Introduction</a></td>
    <td width="20%" align="center"><b>1. Connecting to your F1 instance</b></td> 
    <td width="20%" align="center"><a href="FFMPEG_Lab.md">2. Experiencing F1 acceleration</a></td>
    <td width="20%" align="center"><a href="IDCT_Lab.md">3. Developing F1 applications</a></td>
    <td width="20%" align="center"><a href="WRAP_UP.md">4. Wrapping-up</td>
  </tr>
</table>

---------------------------------------
### Connecting to your F1 instance

In this module you will start a pre-configured EC2 F1 instance and connect to it using a remote desktop client. Once connected, you will download the lab files and confirm you can execute a simple application on F1.

#### Start a preconfigured EC2 F1 instance

For this event, each participant has been attributed an EC2 F1 instance, and login credentials.

You should have received an email that provides you with an account ID, a user name ("user" followed by a number) and a web link to access an EC2 F1 instance.
```
If you have not received that email, please contact a staff member at the beginning of the lab session.
```
- Click on that link, it points to the AWS EC2 console management page.
- Enter the **Account ID** from the email.
- Click **Next**.
- Enter the IAM **user** from the email.
- Enter the password communicated by the staff.
- Click **Sign In**.

You should see one stopped EC2 F1 instance.
- Start the instance by choosing the **Actions** button, then select **Instance State** and then **Start**.

![Start](./images/setup_lab/start1.png?raw=true)

Allow some time for the instance to start. If needed, click the **Refresh** icon (![Refresh](./images/setup_lab/refresh2.png?raw=true)) in the top-right corner of the EC2 dashboard to update the instance status information.

Once the instance is running, the EC2 console gives you information relative to the **public IP address** of the instance which we will be using in the next step.

#### \"Remote desktop\" to the instance

The instance just started is preconfigured with remote desktop protocol (RDP) services.
- From your local machine, start a remote desktop protocol client
   - On Windows: press the Windows key and type "remote desktop".  You should see the "Remote Desktop Connection" show in the list of programs.  Alternatively you could also directly invoke mstsc.exe.
  
   - On Linux: any RDP client such a Remmina or Vinagre are suitable
   - On macOS: Microsoft Remote Desktop from the Mac App Store
- Set your remote desktop client to use **24-bit for color depth** (Option->Display tab for Windows Remote Desktop).
- In the RDP client, enter the **public IP address** you see in the **Description** tab, in the lower part of the **AWS Console Management** web page.
- Click **Connect**. This should bring up a message about connection certificates. 
- Click **Yes** to dismiss the "certificate" window. The Remote Desktop Connection window opens with a login prompt..
- **Login** with the following credentials:
   - User: **centos**
   - Password: ******** _(provided at the event)_
   
    ![Remote](./images/setup_lab/remote1.png?raw=true)
   
- Click **Ok**.

You should now be connected to the instance.

#### Open the lab instructions on the remote F1 instance

* Double click on the Chromium browser icon, it opens to the lab instructions.
  - Note: if a "keyring" popup comes up, click **Cancel**. 
  - We suggest you perform all your copy-paste from the instructions to the shell within the RDP session to avoid issues.


#### Configure the Xilinx SDAccel environment and load the workshop files

* Open a new terminal by right-clicking anywhere in the Desktop area and selecting **Open Terminal**.

* In the termnial shell, execute the following commands to setup the SDAccel environment and `git clone` the necessary lab files.

```bash  
cd /home/centos
git clone https://github.com/Xilinx/SC17_Developer_Lab.git
export AWS_FPGA_REPO_DIR=/home/centos/aws-fpga
cd $AWS_FPGA_REPO_DIR
source sdaccel_setup.sh
source $XILINX_SDX/settings64.sh 
```

#### Run the hello_world example to confirm the setup of your F1 instance

The hello world example is an OpenCL application with a simple vector-addition accelerator. This example uses a precompiled FPGA binary to reduce compilation time and streamline the lab.

*  Compile the host application
```bash
# Go to the example directory
cd ~/SC17_Developer_Lab/helloworld_ocl

# Compile the host application (./helloworld)
make TARGETS=hw DEVICES=$AWS_PLATFORM exe
```

* Confirm the presence of the precompiled FPGA binary.
```bash
ls -la ./xclbin/vector_addition.hw.xilinx_aws-vu9p-f1_4ddr-xpr-2pr_4_0.awsxclbin
```

* Execute the host application with the precompiled FPGA binary on the F1 instance.
```bash
sudo sh
source /opt/Xilinx/SDx/2017.1.rte/setup.sh
./helloworld
```

* A successful outcome looks as follows:
```
Device/Slot[0] (/dev/xdma0, 0:0:1d.0)
xclProbe found 1 FPGA slots with XDMA driver running
platform Name: Xilinx
Vendor Name : Xilinx
Found Platform
Found Device=xilinx:aws-vu9p-f1:4ddr-xpr-2pr:4.0
XCLBIN File Name: vector_addition
INFO: Importing ./vector_addition.hw.xilinx_aws-vu9p-f1_4ddr-xpr-2pr_4_0.awsxclbin
Loading: './vector_addition.hw.xilinx_aws-vu9p-f1_4ddr-xpr-2pr_4_0.awsxclbin'
Result =
42 42 42 42 42 42 42 42 42 42 42 42 42 42 42 42
42 42 42 42 42 42 42 42 42 42 42 42 42 42 42 42
42 42 42 42 42 42 42 42 42 42 42 42 42 42 42 42
42 42 42 42 42 42 42 42 42 42 42 42 42 42 42 42
42 42 42 42 42 42 42 42 42 42 42 42 42 42 42 42
42 42 42 42 42 42 42 42 42 42 42 42 42 42 42 42
42 42 42 42 42 42 42 42 42 42 42 42 42 42 42 42
42 42 42 42 42 42 42 42 42 42 42 42 42 42 42 42
42 42 42 42 42 42 42 42 42 42 42 42 42 42 42 42
42 42 42 42 42 42 42 42 42 42 42 42 42 42 42 42
42 42 42 42 42 42 42 42 42 42 42 42 42 42 42 42
42 42 42 42 42 42 42 42 42 42 42 42 42 42 42 42
42 42 42 42 42 42 42 42 42 42 42 42 42 42 42 42
42 42 42 42 42 42 42 42 42 42 42 42 42 42 42 42
42 42 42 42 42 42 42 42 42 42 42 42 42 42 42 42
42 42 42 42 42 42 42 42 42 42 42 42 42 42 42 42
TEST PASSED
sh-4.2#
```

You compiled a host application and successfully executed it on F1 using a pre-compiled Amazon FPGA Image (AFI).

* Close your terminal
```bash
exit
exit
```

This concludes this first lab.

---------------------------------------

<p align="center"><b>
Start the next module: <a href="FFMPEG_Lab.md">2: Experiencing F1 acceleration</a>
</b></p>
