# Honeypot Assignment

**Time spent:** **6** hours spent in total

**Objective:** Create a honeynet using MHN-Admin. Present your findings as if you were requested to give a brief report of the current state of Internet security. Assume that your audience is a current employer who is questioning why the company should allocate anymore resources to the IT security team.

### Milestone 1: Create MHN Admin VM ###

Start by creating the MHN Admin VM via your cloud provider. The VM needs to have an internet-facing IP and accessible to you via SSH. The MHN Admin VM will be provisioned with the following attributes:

    Ubuntu 18.04 Minimal
    HTTP traffic allowed (port 80)
    TCP ports 3000 and 10000 need to be open to allow incoming (aka 'ingress') traffic for geolocation and honeypot sensor data.

That last requirement is generally the only one that may require a specific firewall rule to configure properly, because those ports are non-standard and specific to MHN. Some cloud providers may require you to create the firewall rules separately and then apply them to the VM. Either way, make sure when you create the VM that you can access it via SSH.

<img src="mhn-admin.gif">

### Milestone 2: Install the MHN Admin Application ###

After having established SSH access the MHN Admin VM, the following instructions can be run on the remote VM to install the application. Note: this step may take 30-40 minutes overall. These instructions were adapted from the MHN README


<img src="dionaea-honeypot.gif">

### Milestone 3: Create a MHN Honeypot VM ###

MHN supports multiple honeypots, each of which has a slightly different purpose you can read about. To start, we'll deploy Dionaea over HTTP, a honeypot used to trap malware samples.

First, create a VM for your first honeypot via your cloud provider. As before, this VM also needs to have an internet-facing IP and accessible to you via SSH.

This VM will require different ports open, though which ones depend on the specific honeypot being used. To keep things simple, for this VM (and any additional honeypot VMs you create), simply allow incoming traffic from all ports and protocols. Again, this will likely require a firewall rule.


### Milestone 4: Install the Honeypot Application ###

After having established SSH access the new honeypot VM, we need to install the honeypot application into the VM and wire it to connect back to the admin server. Fortunately, MHN makes this fairly straightforward. First, in the MHN admin console in your browser, click on Deploy in the top nav, and you'll be asked to select a script. Choose Ubuntu/Raspberry Pi - Dionaea, and you'll see a Deploy Command appear with a full deployment script below it. You can ignore the script, which is just for reference, but make a note of the Deploy Command, which is the one-line command you'll need to execute inside the honeypot VM you connected to in the last step.

So, copy the command from the browser page. It should start with wget and end with a unique token string. Execute this command inside the honeypot VM to install the Dionaea software. It shouldn't take more than a few minutes to complete. When it's done, click back over to the MHN admin console in your browser. From the top nav, choose Sensors >> View sensors and you should see the new honeypot listed.

**Summary:** What does this honeypot simulate and do for a security researcher?

<img src="x-honeypot.gif">

### Milestone 5: Attack! ###

Now for the fun part: let's attack the honeypot to make sure it's all working. You can use Nmap in Kali Linux and pass it the IP of the honeypot VM (not the IP of the MHN Admin VM):

<img src="x-malware.gif">

## Notes

Describe any challenges encountered while doing the assignment.
