# Getting to Grips with Monero - Setting up your own Node 

## PREREQUISITES

* gpg2 (Linux)
* Kleopatra / gpg4win (Windows)
* At least 50 GB disk space

<hr/>

### INTRO

Hello and welcome to the second video in the "Getting to grips with Monero" series

In this video, we'll be developing our understanding of nodes, the most important piece of infrastructure in the Monero ecosystem

We'll be discussing what they are, why they're important and demonstrating step-by-step how to set up your own.  So let's get going!


### WHAT IS A MONERO NODE?

Fundamentally a Monero node is a piece of hardware connected to the Internet that both stores a copy of the blockchain and runs the Monero software

Running your own node and connecting to the P2P network is kind of like downloading and seeding a torrent for all those who want to use it

Nodes are programmed to follow a certain set of rules which facilitate the running of the network. An important abstraction from these rules is the consensus mechanism. 

It's through this mechanism that the legitimate history of the Monero blockhain is maintained.  The greater the number of nodes in the network, the more resilient it is against both denial of service attacks and network partitioning. 

Nodes are typically separated into two categories: 
1.  *Local nodes* are those **within** your local network
2.  *Remote nodes* are those **outside** your local network


### REMOTE VS LOCAL

There are a few benefits to running a local node, the most notable of which is maintaining your privacy! 

When you connect to remote nodes, it's possible for the host to obtain the following details about you: 
- IP address
- Block height from which your wallet started synchronisation
- Transaction IDs you broadcast and a list of decoys

Depending on your privacy concerns, this might not be ideal.  So make sure you connect to a remote node hosted by someone you can trust. This is very important!

If you are unable to run your own node for whatever reason, you can skip over this video for now.

Another thing to think about, either when connecting to remote nodes or hosting your own, is that your Internet Service Provider (ISP) will be able to recognise all of your activities. Although this information doesn't deanonymise your Monero address or transactions, it can still be used by malicious actors. 

Hosting your own node for use with your own wallet simply reduces the amount of your personal data floating around the web. Monero's Dandelion++ technology does the hard part by seamlessly obfuscating the origin of all transactions. [This article](https://localmonero.co/knowledge/monero-dandelion) from the good folks at LocalMonero goes into more detail about Dandelion++.

Before we continue, you need to be learn about whatever local risks, if any, are associated with hosting your own node.  This is important for your personal security and obviously depends on where in the world you live and work. 

Currently, the best ways to shield your Internet activities from malicious actors is through a trustworthy Virtual Proxy Network (VPN), Tor routing (The Onion Routing Project) or Invisible Internet Project (I2P). Best practices are not timeless and there will always be developments in the web and the Monero ecosystem, but the Monero developer community is one of the largest and most privacy-focused organizations in this space.

Please skip to the next video if you have any security concerns. If you still want to host your own node and support the network, we will of course be showing you how to do so with VPN in Video 4 of this series: **Using Monero with Enhanced Privacy**.


### HARDWARE RECOMMENDATIONS

Most users run their nodes 24/7, so plan on operating low-powered and efficient hardware using "System On Chip" (SOC) architechture from AMD or Intel

Generally speaking, the Rasberry Pi and other ARM-based (Advanced RISC Machine) systems would be ideal for something like this. However, it's not the best platform for running the Monero daemon as the hardware lacks support for the "Advanced Encryption Standard" (AES) instruction set. This major disadvantage leads to drastically longer sync times. Typically, only systems with x86 architecture benefit from this instruction set.

The Monero daemon requires 1 to 2 GB of memory to run, so aim to use a system with at least 4 GB or memory

If you're planning on using a single board computer like the Raspberry Pi and are feeling adventurous, we would recommend following this [guide](https://moneroecosystem.org/pinode-xmr/) published by the good folks from the Monero ecosystem work-group.


### DOWNLOADING THE MONERO SOFTWARE

Download your node software from the official [github repository](https://github.com/monero-project/monero/releases), or just click the link in our video description.  Assuming you followed all the steps from our last video, *Importing Public Keys and Verifying Hashes*, you will be ready to proceed with validated official Monero node software!

If you haven't, please make sure you do that now. You'll find the video listed in the *Getting to Grips with Monero* playlist 

The next sections will cover the different steps in the installation process for both Linux and Windows.  Use the time stamps below to jump to the parts you need.


### PREPARING YOUR FOLDERS - LINUX

If you are using a linux distro like I am currently, then you're going to need to open a command line terminal. I'm going to navigate to the right directory using the terminal and the change directory command: `cd`. You can then use `ls` to check you're in the right place. If you're using the file explorer, head to the proper folder and *Right click* and select *Open in Terminal*.

You'll find the commands used in the description below, feel free to copy and paste them into your terminal window. To paste into the terminal window you'll probably need to use the *Shift* key in addition to *Ctrl* key to copy (*Ctrl + Shift + C*) and paste (*Ctrl + Shift + C*). 

`mkdir ~/monerod; tar -xjf monero-linux-x64-v*.tar.bz2 -C ~/monerod`

Let's break down this command. First, we're making a directory called *monerod*, in the user's directory (`/home/"USERNAME"`), then we're using the `tar` function to unpack the compressed folder into the directory we just created.

Now, let's run that by hitting *Enter*

Use the `cd` command and navigate to the newly created directory and look for the extracted folder using the `ls` command


### PREPARING YOUR FOLDERS - WINDOWS

The first thing we're going to do is move download file to a custom folder. First select and cut using *Ctrl+X*

Next we'll go to the `C:` drive to create a folder called *monerod*. Double click on the new folder and paste the zip file you just cut with *Ctrl+V*

Double click the zip file to open, then drag and drop the folder into the address bar, onto the name of the parent folder.  Open the *monerod* folder when finished.

As Windows users it's best to add a custom security rule to your virus and threat protection settings to avoid any complications when running your node:

- First, open the virus and threat protection settings by typing in the search bar or opening the start menu and typing in `virus`
- Next, under *Virus and Threat Protection Settings*, click on *Manage Settings*
- Scroll down until you see the *Exclusions* Section and choose *Add or remove exclusions*
- Click *Add an exclusion*
- Choose *Folder*
- Then select the folder that you just created in the root directory


### CREATING A CONFIG FILE

Creating a config file is a pretty simple way to tailor the Monero daemon to suit your own situation. There is no default config file, so we'll be creating this from scratch by referring to the documents hosted on [monerodocs.org](www.monerodocs.org).

In the monerod folder create a file called *bitmonero.conf*, this can be opened and edited with any text editor 

We're going to use [the example file](https://monerodocs.org/interacting/monero-config-file/) from MoneroDocs as the template

Please click on the subheading *Examples* and copy the example to your clipboard using the provided button. Now paste it into your text editor.

You'll notice quite a few *#* symbols in this text. These are comments. Every time the Monero daemon comes across one, it ignores it and skips to the next line. It's a really easy way for us to leave information and comments in the file without them interfering with its operation.

There are a lot of different settings you can apply to the daemon and the [MoneroDocs Reference Page](https://monerodocs.org/interacting/monerod-reference) is a great resource for learning more


### TO PRUNE OR NOT TO PRUNE

The first option we see here enables us to set the location of the blockchain. This requires a little thought because the database that contains the monero blockchain is rather large and ever-growing.

One of the prerequisites for this video was at least 50 GB of disk space, this is the minimum required space and would only allow you to download a pruned version of the blockchain, not the entire thing!

A pruned node is one with the entire transaction history but only about 1/8th of the details. For this reason, not all pruned nodes are created equal and only together can they preserve the transaction history of the entire blockchain

Pruned nodes are always recommended when connecting remotely, but if you have the space it's a big help to the network if you host a full node at 130 GB (and growing)!

To set the location of the blockchain you need to edit everything after the **`=`** sign. Make sure you include the full directory path, including the drive letter if you're using Windows. I'm going to leave it as default for now.

If you want to download a pruned copy of the blockchain we need to add a few more lines, first I'm going to add a subheading starting with `**#**` called *Custom*, this way I remember that I added the following lines myself. Underneath we're going to add `sync-pruned-blocks=1` and `prune-blockchain=1`. The value **`1`** indicates we want to enable this option. If you want to disable them, you can either add a **`#`** to the start of the line (to comment it out) or change **`1`** to **`0`**.


### FINALISING OUR CONFIG FILE

Before we take a look at the rest of the file, we're going to add two more lines to our custom list; `enable-dns-blocklist=1` and `no-zmq=1`. Enabling the block list prevents connections to known bad actors and is centrally maintained by the Monero core team. The `no-zmq` option disables a particular interface we will not be using, limiting the potential attack surface.

The first setting in the default config sets the location of the database file which will be created to store the blockchain data. I'm going to set it so that it saves it to a new folder called *data* within the *monerod* folder we created earlier. To do this we can simply replace this location with *data*.

The next thing on the list is the location you want the Monero daemon to save logs. I'm going to change this to the same data folder by deleting everything that comes before section titled *monerod.log*.  If anything goes wrong, we can quickly and easily investigate from here!

Before continuing, let's consider whats actually going on here when the node is spinning up

Every time you start the Monero daemon it starts several processes which use different ports to run. The first of these is the P2P service. This is how your node communicates with the rest of the network and keeps itself up-to-date. Currently the IP address is bound to **`0.0.0.0`**, this is the best option if you haven't got any kind of custom networking. 

The port number is bound to the default recommendation. You can of course change this to what ever you like, but be mindful that a wide variety of ports are used by other applications/services, so it's a good idea to stick to the recommended ones. 

Being able to change this port number is great if you cannot forward a certain port on your router or if your VPN service requires a certain value

However for now, leave this port as default.  For our node to be a fully-fledged member of the Monero network we need to ***forward this port on both our firewall and router*** so that our node can shake hands with other nodes.

The other process on the list is the Monero RPC, or Remote Prcedure Call. RPC is the method used for communication between wallets and nodes. We're not going to go into too much detail in this video, but it is possible for you to allow external connections. Running an RPC service is certainly helpful for those who don't run their own node, but it exposes an entirely different part of the Monero codebase to the internet. As many of you will be setting this up on your own personal computer, we advise against this for now.

To save time in this video we're going to skip over the next two sections in the config file. If you're interested in what they do, please check out MoneroDocs for more info.

Finally we move onto network traffic. How many peers you connect to and the bandwidth you allocate is totally customisable. The more outpeers and the down rate will directly contribute to your initial sync. So I suggest you have these pretty high to begin with. You can always change things later on to suit your circumstances. 
I'm going to leave all of this as default for now.


### SPINNING UP YOUR NODE

The next thing we're going to want to do is change the location of the *monerod program*. You can do this through the file explorer or terminal, it's up to you. You need to be sure that either the monerod binary or monerod.exe is now located in the *monerod* folder alongside the config file. 

***CAUTION**:  Each time you download an updated copy of the software, you will need to replace this file!*

After all our work we can start our node for the very first time. Using the terminal, go to the *monerod folder*:

Windows:
- *Shift + Right Click*
- Open up a powershell
- Type  `./monerod.exe --config-file=./bitmonero.conf`

Linux:
- *Right Click*
- Open a terminal
- Type `./monerod --config-file=./bitmonero.conf`

Now let's hit *Enter*!

As you can see from the messages, we are now syncing the blockchain to your computer! 

This is a pretty lengthy process so be prepared. You can take a break from it whenever you like by using the command *Ctrl + C*. This command will cancel the operation. To start it again from where you left off, simply follow the same process.

Currently we are only leaching the blockchain from the P2P network and sharing is caring after all, so we'll want to enable seeding as well, right?

To do this, we're going to have to set special rules in the firewall to allow incoming connections for the p2p port, **`18080`** on our computers and router

This may or may not be technically possible for you, as it depends on your ISP and your administrative access to the router.

The following two sections will cover Linux and Windows independently, so please head to the appropriate section. As for routers, please take a look at your manufacturers recommendations. If you're currently using a VPN, please take a look at our video *Using Monero With Enhanced Privacy* as things will be a little bit different for you.


### FORWARDING THE P2P PORT - LINUX

Forwarding the required port is relatively simple as a Linux user. To do so, we're going to use the [Uncomplicated Firewall (UFW)](https://wiki.ubuntu.com/UncomplicatedFirewall). This may be entirely new to you and if it is, you will first want to see if it's installed on your system.

Open up a new terminal and type `ufw --version`. If you don't get a printout with a version number you'll need to install it, which you can do via your package manager.

Now let's enter these three commands:
1. Enable the UFW:
   `sudo ufw enable`
2. Block incoming connections:
   `sudo ufw default deny incoming`
3. Allow all outgoing connections:
   `sudo ufw default allow outgoing`
   
This isn't ideal right now as you won't be able to use your browser or download system updates. For this reason you're going to want to **allow ports `443` (tcp-https) and `80` (tcp-http)**. To do this you need to run the command:

`sudo ufw allow 80/tcp` & `sudo ufw allow 443/tcp`

Now that the UFW has been enabled and your firewall has been hardened, your computer is a little more secure and we're ready to make an exception for the Monero daemon:

`sudo ufw allow 18080/tcp`

This command will allow traffic to access your monero daemon, you may remember this port number from the config file we created earlier. After you press enter you should see system message saying *rule added*. To double check that it worked, run `sudo ufw status`. We can see it listed in the printout, so everything went fine.

Well, that's all there is to it for your PC. The only thing left to do is forward the port on your router. Every router is different, so please have a look at your manufacturer's instructions for this step.


### FORWARDING THE P2P PORT - WINDOWS

To begin, click on the Windows start menu and type `firewall`.  Click on the result from Windows defender.

Once open, head to advanced settings and choose inbound rules in the left hand column. Next select *New rule* under the *actions* subheading.

Here we need to select *Port* and then *Next*. The protocol we're interested in is *tcp* and now we need to specify the port used by the Monero daemon which is **`18080`**

In the next menu, we want to select *Allow the connection*. Now it's time to name the rule *Monerod P2P* before clicking the *Finish" button.

That's it, we've opened up our port in Windows for the Monero daemon to communicate with the rest of the network.

The only thing left to do is forward the port on your router. Every router is different, so please have a look at your manufacturers instructions for this step.


### CHECKING OUR PROGRESS

On a 100 Mbit connection writing to an SSD, it's taken me a little over a day to sync the entire blockchain. Once it's synced you should see the message **`SYNCHRONISED OK`**.

We can confirm the status of our nodes by using the `status` command. This shows the height of the blockchain and a few other bits, including the number of incoming and outgoing connections.

Another neat command is `print_net_stats` which lets us see how much data has been received and contributed to the network and at what rate.

Of course no Internet connection is the same and you may want to limit your traffic. You can do so on the fly or by editing the config file we set up earlier. Take the time to find the settings that really suit your needs!

If you're interested in seeing what else you can do whilst the daemon is running type `help`

As the initial sync is complete, I'm going to limit my traffic. I'm going to offer 1 Mb/s to my incoming connections and 1.5 Mb/s to outgoing as I use my PC for many other things. I'm going to do so using the `limit_up` and `limit_down` commands.

Once again, please take a look at [MoneroDocs](https://monerodocs.org/interacting/monerod-reference/#commands) for more documentation. It has lots of useful information for helping tune your node!


### CONCLUSION

Well, there we have it, our very own node!

Now we can rest easy knowing that we're supporting the network and have the basis for all our future Monero needs!

If you have any comments or questions, feel free to leave them below, but please search for similar questions before doing so.

That's it for this video, if you're interested in seeing how you can put your node to use, you can check out the other videos in this series.

Thanks for watching and bye for now.

