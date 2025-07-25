<h1> Tenable: Authenticated vs Unauthenticated Scans on a Linux Host </h1>
</hr>


[Watch the Video Tutorial](https://youtu.be/2TwhvOKBmGY?si=XIfpKhDhXkGYqmuJ)


<hr>



<details open>
<summary><strong> Virtual Machine Step by Step Configuration Tutorial </strong></summary>

  <br>
  
<strong > Step 1:   Azure Portal → Virtual machines (Either Search for Virtual Machines or Click the button) </Strong>

This is where all existing VMs live and where you’ll create new ones.

<img src="https://i.imgur.com/BwckhEn.png">

  <br>
  
<strong> Step 2:   Click Create → Virtual machine.</Strong>
For this lab you only want a single Windows box (not a scale set or preset image).

  <br>
  
<img src="https://i.imgur.com/I5W5r2u.png">


<img src="https://i.imgur.com/KkvEQj3.png">

  <br>

<strong > Step 3: Basics Tab:</strong> 

<ul> <strong> Subscription: </strong> choose the one your accounts billed under, your organization's config will vary </ul>

<ul> <strong> Resource group:</strong> pick an existing resource Group (or if you do bot have one click Create new, note we will not be covering the creation of Resource Groups in this tutorial) </ul>

Resource Groups keep everything that belongs to this VM together, so you can manage/clean them up as a unit.

  <br>

<img src="https://i.imgur.com/Xl8SZtP.png">

  <br>

<strong > Step 3.1: VM Name & Region:</strong> 


<ul> <strong> Name: </strong> cName it so you instantly know its purpose. It can be confusing once you have several VMs going if you do not have a good naming convention </ul>

<ul> <strong> Region: </strong> cusually pick the closest region to you (lower latency) and where your quotas allow creating this image/size every organization is different so your selection may vary </ul>

<ul> <strong> Availability options / Zones & Security type  </strong> Leave these Default we will not be altering them at this time, Availability Zones primarily pertain to Datacenters and Security Type allows for options like Secure Boot which we will not be relevant in this tutorial  </ul>

  <br>



  <br>


<strong > Step 3.2: VM Name & Region:</strong> 


<ul> <strong> Image: </strong> Windows 10 Pro, 22H2, x64 Gen2 </ul>

Windows 10 desktop-like target to RDP into (often used for defender / vuln scan labs). For servers, pick Windows Server images instead.

<ul> <strong> Size : </strong> Standard_DS1_v2 (1 vCPU, 3.5 GiB RAM) </ul>

This will likely vary based on your Permissions/Role within your organization some will allow for you to use more VCPUs others will not, for this we will continue with the cheapest option

<ul> <strong> Administrator account  </strong> Set a username + strong password.  </ul

 Please make a note that this should be a secured account, This lab will be connected to the public internet meaning it is very possible for your VM to be hacked and cause damage to other people if you are not careful, always exercise caution and remember to tear down this Vm when finished.

<ul> <strong> Inbound ports: </strong> Allow selected ports → RDP (3389) </ul>

This opens RDP to the whole internet. Great for a quick lab, unsafe for real world environments

<ul> <strong> Licensing checkbox : </strong> Check the “I confirm I have an eligible Windows 10/11 license with multi-tenant hosting rights.” box </ul>

Microsoft requires you to attest you’re properly licensed to run Win 10/11 as a VM in Azure. If you don’t have that right, use Windows Server or a pre-licensed Win10/11.

  <br>

<img src="https://i.imgur.com/KeEUhao.png">

<img src="https://i.imgur.com/TqHDSCb.png">

  <br>

<strong > Step 4: Disks tab :</strong> 

  <br>

<ul> <strong> OS disk type: Standard HDD (LRS) </strong> Cheapest. Fine for a low IO lab box in real world environments this would likely be different, we are choosing this for the cheapest option</ul>

<ul> <strong> Delete with VM: Checked: </strong> When you delete the VM, Azure also deletes the disk so you don’t keep paying. </ul>

<ul> <strong> Next Click Networking  </strong> </ul>

  <br>
  
<img src="https://i.imgur.com/SrUg97U.png">

  <br>


  <br>
<strong > Step 5: Networking tab  :</strong> 

  <br>
<ul> <strong> Virtual Network </strong> Select the Virtual Network, this lab assumes you have one available to you, if you don't you will need to provision one. This will allow us to place the VM into a Virtual Network/ul>

Then ensure your Subnet and Public IP are created. This will allow us to communicate with traffic not in our network. 

<ul> <strong> NIC network security group: Basic </strong> Azure will build a simple NSG for you that allows 3389 since you picked it on Basics. </ul>

<ul> <strong> Delete public IP and NIC when VM is deleted  </strong> Good practice reduces time on having to do this manually later </ul>


<ul> <strong> Click Next into the Monitoring Tab </strong>  </ul>
  <br>
  
<img src="https://i.imgur.com/XSXF6zr.png">

  <br>
<strong > Step 6: Monitoring tab  :</strong> 
  <br>

<ul> <strong> Boot diagnostics: Disable  </strong> Just not relevant for the content of this lab /ul>

<ul> <strong> Leave the rest (guest diagnostics, health) unchecked.</strong> </ul>

<ul> <strong> Click Review + create, pass validation, then Create. </strong>  </ul>


  <br>
<img src="https://i.imgur.com/bnytFcd.png">

  <br>
<strong > Step 7:Deployment:</strong> 
  <br>

<ul> <strong> Deployment complete → Go to resource  </strong> Once the VM is live go to the Overview blade after clicking the Go to resource button  </ul>

<ul> <strong> Make Note of the Private and Public IP addresses</strong>  We will be using the Public IP to Remote into the VM with RDP or Azures Bastion Platform.</ul>

<ul> <strong> StartUp RDP and enter in the Public IP information and accept the self signed certificate </strong>  </ul>

  <br>
<img src="https://i.imgur.com/BYTeC6K.png">
<img src="https://i.imgur.com/eh1mNVn.png">
<img src="https://i.imgur.com/IaGbbQP.png">
  <br>
