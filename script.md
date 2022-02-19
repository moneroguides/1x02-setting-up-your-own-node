# Getting to Grips with Monero, Video 2 

## PREREQUISITES

* gpg2 (Linux)
* Kleopatra / gpg4win (Windows)
* At least 50 GB disk space

<hr/>

### INTRO

Hello and welcome to the second video in the "Getting to grips with Monero" series

In this video, we will be developing our understanding of nodes, the most important piece of infrastructure in the Monero ecosystem

We'll be discussing what they are, why they're important and demonstrating step-by-step how to set up your own, so let's get going!


### WHAT IS A MONERO NODE?

Fundamentally a Monero node is a piece of hardware connected to the Internet which both stores a copy of the blockchain and runs the Monero software

Running your own node and connecting to the P2P network is kind of like downloading and seeding a torrent for all those who want to access it.

Nodes are programmed to follow a certain set of rules which facilitate the running of the network. An important abstraction from these rules is the consensus mechanism. It is through this mechanism that the legitimate history of the Monero blockhain is maintained.

The greater the number of nodes in the network the more resilient it is against both denial of service attacks and network partitioning. 

Nodes are typically separated into two categories, local and remote. Local nodes are those within your local network while remote nodes are those outside your local network.


### REMOTE VS LOCAL

There are a few benefits to running a local node, the most notable of which is privacy! 

When you connect to remote nodes, it is possible for the host to obtain the following details: Your IP address, the block height from which your wallet started synchronisation, the transaction IDs you broadcast and a list of decoys. Depending on your own privacy concerns, this might not be ideal.

That being said, if you are unable to run your own node for whatever reason, you can skip over this video for now. Just make sure you connect to a remote node hosted by someone you can trust. This is very important!

Another thing to think about, either when connecting to remote nodes or hosting your own, is that your Internet Service Provider (ISP) will be able to recognise this. Although this information doesn't deanonymise your address or your transaction, it may still be used in a malicious way. 

Hosting your own node for use with your wallet simply reduces the amount of data floating around the net. Monero's Dandelion++ technology does the hard part by obfuscating the origin of transactions. [This article](https://localmonero.co/knowledge/monero-dandelion) from the folks at LocalMonero goes into more detail.

Before you continue, be sure that you understand the risks, if any, associated with hosting your own node. These may be different depending on where in the world you live. 

In order to hide your use of the Monero network, the best ways of doing so are through a trustworthy virtual proxy networks (VPNs), The Onion Routing (Tor) Project or Invisible Internet Project (I2P). Please skip to the next video if you have any concerns; if you still want to host your own node and support the network, we will be demonstrating a method via VPN in the final video **Using Monero with Enhanced Privacy**.

Best practice is not timeless. There are always developments in the Monero ecosystem, all of which go toward creating a better user experience for the Monero community.


### HARDWARE RECOMMENDATIONS

Running your node 24/7 is of most benefit to the Monero network and for most, it's not practical or environmentally friendly to run nodes on powerful and ineffcient machines.

It is for this reason we would primarily like to reccomend the use of low powered and effcient architechture like the "system on chip" (SOC) designs from AMD and Intel.

Generally speaking the Rasberry Pi and other ARM based systems would be ideal for something like this. However, it is in fact not the best platform for running the Monero daemon. This is because the hardware lacks support for the "Advanced Encryption Standard" (AES) instruction set. The major dissadvantage is drastically longer sync times. Typically, only systems with x86 architecture will benifit from this instruction set.

The Monero daemon can require between 1 and 2 GB of memory to run. So any system should ideally have around 4GB of memory.

If you are planning on using a single board computer like the Raspberry Pi and are feeling adventurous, we would recommend this [guide](https://moneroecosystem.org/pinode-xmr/) published by the good folks from the monero-ecosystem work-group. be aware that there may be a more up to date version when you watch this video.


### DOWNLOADING THE MONERO SOFTWARE

The software required to run a node can be found on the official [github repository](https://github.com/monero-project/monero/releases), the link for which can be found in the video description.

If you followed all of the steps from our other video, 'importing public keys and verifying hashes', you should have already downloaded and verified these files.

If you haven't, please make sure you do that now. You will find it in the playlist labelled "Getting to Grips with Monero".

The next sections will cover the process for Linux and Windows independently, please use the time stamps below to get to the part that suits you.


### LINUX - GUIDE

If you are using a linux distro like I am currently, then you're going to need to open a command line terminal. I'm going to navigate the right directory using the terminal and the change directory command: `cd`. You can then use `ls` to check you're in the right place. If you're using the file explorer, head to the right folder and `right click` and select "Open in Terminal".

You'll find the commands used in the description below, feel free to copy and paste them into your terminal window. To paste into the terminal window you will probably need to use the `shift` key in addtion to `ctrl` to copy (`ctrl + shift + c`) and paste (`ctrl + shift + v`). 

`mkdir ~/monerod; tar -xjf monero-linux-x64-v*.tar.bz2 -C ~/monerod`

Before we execute this command, let's have a little look at what we're about to do. Firstly, we're making a directory called "monerod", in the users directory (/home/"USERNAME"), then we're using "tar" to unpack the compressed folder into the directory we just created.

Now, let's run that by hitting enter.

If we use the `cd` command and navigate to the newly created directory, we can see the extracted folder using the `ls` command once more.


### WINDOWS - GUIDE

The first thing we're going to do is move (cut) the zip file we've downloaded. To do this, we're going to highlight the zip file and press `ctrl+x`

Now we're going to navigate to the `C:` drive and create a folder called "monerod". Double click on the new folder and paste the zip file inside using `ctrl+v`

There are lots of ways to extract the contents of this zip file, and one of the easiest is to double click on the zip file, then drag the folder and drop it on the address bar, on to the name of the parent folder.

Now return to the monerod folder when you're done.

As windows users it's best to add a rule to your virus and threat protection settings to avoid any complications when running your node.
To do this we'll need to go to the virus and threat protection settings. You can find this by typing it in the search bar or opening the start menu and typing in `virus`. Next, under Virus and Threat Protection Settings, click on Manage Settings. Scroll down until you see the "Exclusions" Section and choose "Add or remove exclusions". Click "Add an exclusion", choose "folder" and then navigate to the folder that you just created in the root directory.


### CREATING A CONFIG FILE

Creating a config file is a pretty simple way to tailor the Monero daemon to suit your own needs and circumstances. There is no default config file, so we'll be doing this from scratch using the documents hosted on [monerodocs.org](www.monerodocs.org) as a reference.

In the monerod folder create a file called "bitmonero.conf", this can be opened and edited with any text editor so we won't be covering OS specific details here.

We're going to use [the example file](https://monerodocs.org/interacting/monero-config-file/) from MoneroDocs as a template to work from.
Please click on the subheading "Examples" and copy the example to your clipboard using the provided button. Now paste it into your text editor.

You'll notice quite a few "#" symbols in this text. These are comments. Every time the Monero daemon comes across one, it ignores it and skips to the next line. It's a really easy way for us to leave information and comments in the file without them interfering with its operation.

There are a lot of different settings you can apply to the daemon and the [MoneroDocs](https://monerodocs.org/interacting/monerod-reference) web page is a great resource for finding the things you want.


### TO PRUNE OR NOT TO PRUNE

The first option we see here enables us to set the location of the blockchain. This requires a little thought because the database that contains the monero blockchain is rather large, and ever-growing.

One of the prerequisites for this video was at least 50GB of disk space, this is the minimum required space and would only allow you to download a pruned version of the blockchain, not the entire thing.

Simply put; a pruned node is one with the entire transaction history, but only a small share of the details. Not all pruned nodes are created equal, only together can they preserve the whole blockchain as each holds about 1/8^(th) of the required detail.

Pruned nodes are always recommended over using remote ones, however if you have the space it's a big help for the network if you host a full node. A full node would require around 130GB currently, but this size is always increasing.

To set the location of the blockchain you need to edit everything after the **=** sign. Make sure you include the full directory path, including the drive letter if you're using windows. I'm going to leave it as default for now.

If you want to download a pruned copy of the blockchain we need to add a few more lines, first I'm going to add a subheading starting with **#** called Custom, this way i remember that I added the following lines myself. Underneath we're going to add `sync-pruned-blocks=1` and `prune-blockchain=1`. The value **1** indicates we want to enable this option. If you want to disable them, you can either add a **#** to the start of the line to comment it out or change **1** to **0**.


### FINALISING OUR CONFIG FILE

Before we take a look at the rest of the file, we're going to add two more lines to our custom list; `enable-dns-blocklist=1` and `no-zmq=1`. Enabling the block list prevents connections to known bad actors and is centrally maintained by the Monero core team. The **no-zmq** option disables a particular interface we will no be using, limiting the potential attack the surface.

The first setting in the default config sets the location of the database file which will be created to store the blockchain data. I'm going to set it so that it saves it to a new folder called data in the "monerod" folder we created earlier. To do this we can simply replace this location with "data".

The next thing on the list is the location you want the Monero daemon to save logs. I'm going to change this to the same data folder by deleting everything that comes before section that reads "monerod.log". That way, if anything goes wrong, we can quickly and easily investigate.

Before moving onto the next part of the config it would be good if we address a few things first. Every time you start the Monero daemon it starts several processes which use different ports to run. The first of these is the P2P service. This is how your node communicates with the rest of the network and keeps itself up to date. Currently the IP address is bound to **0.0.0.0**, this is the best option if you haven't got any kind of custom networking. 

The port number is bound to the default and recommended one. You can of course change this to what ever you like, but be mindful that a wide variety of ports are used by other applications/services, so it's a good idea to stick to the recommended ones. 

Being able to change this port number is great if you cannot forward a certain port on your router, or if your VPN service won't let your specify this one, however, we're going to leave this port as default for now, so take note of it. For our node to be a fully fledged member of the Monero network we need to forward this port on both our firewall and router so that our node can relay its blockchain data.

The other process on the list is the Monero RPC. RPC stands for remote procedure call and is the method used for communication between wallets and nodes. We're not going to go into too much detail in this video, but it is possible for you to allow external connections. Running an RPC service is certainly helpful for those who don't run their own node, but it exposes an entirely different part of the Monero codebase to the internet. As many of you will be setting this up on your own personal computer, we advise against this for now.

To save time in this video we're going to skip over the next two sections in the config file. If you're interested in what they do, please check out the monerodocs for more info.

Finally we move onto network traffic. How many peers you connect to and the bandwidth you allocate is totally customisable. The more outpeers and the the down rate will directly contribute to your initial sync. So I suggest you have these pretty high to begin with. You can always change things later on to suit your circumstances. 
I'm going to leave all of this as default for now.


### SPINNING UP YOUR NODE

The next thing we're going to want to do is change the location of the monerod program. You can do this through the file explorer or terminal, it's up to you. You need to be sure that either the monerod binary or monerod.exe is now located in the "monerod" folder alongside the config. Each time you download an updated copy of the software, you will need to replace this file.

After all our work we can start our node for the very first time. Using the terminal, navigate to the folder that the monderod program is located in, then:

**for Windows:**
- `shift+right click`
- open up a powershell
- type  `./monerod.exe --config-file=./bitmonero.conf`

**for Linux:**
- `right-click`
- open a terminal
- type `./monerod --config-file=./bitmonero.conf`

Now let's hit enter!

As you can see from the messages, we are now syncing the blockchain to your computer. 

This is a pretty lengthy process so be prepared. You can take a break from it whenever you like by using the command `ctrl+c` to cancel the operation. To start it again from where you left off, simply follow the same process.

Currently we are only leaching the blockchain from the P2P network and sharing is caring after all, so we'll want to enable seeding as well.
To do this, we're going to have to set special rules in the firewall to allow incoming connections for the p2p port (18080) on both our computers and routers.

This may or may not be technically possible for you. This will all depend on your ISP and aministrative access to your router.

The following two sections will cover linux and windows independently, so please head to the appropriate section. As for routers, please take a look at your manufacturers recommendations. If you're currently using a VPN, please take a look at our video **Using Monero With Enhanced Privacy** as things will be a little bit different for you.


### FORWARDING THE P2P PORT - LINUX

Forwarding the required port is relatively simple as a linux user. To do so, we're going to use the [Uncomplicated Firewall](https://wiki.ubuntu.com/UncomplicatedFirewall), ufw for short. This may be entirely new to you and if it is, you will first want to see if it's installed.

Open up a new terminal and enter `ufw --version`. If you don't get a printout with a version number you'll need to install it, which you can do via your package manager.

Now let's enter these three commands:

1. Enable the ufw:
   `sudo ufw enable`
2. Block incoming connections:
   `sudo ufw default deny incoming`
3. Allow all outgoing connections:
   `sudo ufw default allow outgoing`
   
This isn't ideal right now as you won't be able to use your browser or download system updates. For this reason you're going to want to allow ports 443 (tcp-https) and 80 (tcp-http). To do this you need to run the command:

`sudo ufw allow 80/tcp` & `sudo ufw allow 443/tcp`

Now that the ufw has been enabled and your firewall has been hardened, your computer is a little more secure and we're ready to make an exception for the Monero daemon:

`sudo ufw allow 18080/tcp`

This command will allow traffic to access your monero daemon, you may remember this port number from the config file we created earlier. After you press enter you should see "rule added." To double check that it worked, you can run `sudo ufw status`. We can see it listed in the print out, so everything went fine.

Well, that's all there is to it for your PC. The only thing left to do is forward the port on your router. Every router is different, so please have a look at your manufacturer's instructions for this step.


### FORWARDING THE P2P PORT - WINDOWS

To begin, click on the windows start menu and type firewall, click on the result from windows defender.

Once open, head to advanced settings and choose inbound rules in the left hand column. Next select "new rule" under the actions sub heading.

Here we need to select "port" and then "next". The protocol we're interested in is "tcp" and now we need to specify the port used by the Monero daemon which is `18080`

In the next menu, we want to select "Allow the connection". Now it's time to Name our Rule, I suggest Monerod P2P, finally, hit the finish button.

That's it, we've opened up our port in wodows for the Monero daemon to communicate with the rest of the network.

The only thing left to do is forward the port on your router. Every router is different, so please have a look at your manufacturers instructions for this step.


### CHECKING OUR PROGRESS

On a 100Mbit connection and writing to an ssd, it's taken me a little over a day to sync the entire blockchain. Once it's synced you should see the message **SYNCHRONISED OK**.

We can confirm the status of our nodes by using the command `status`. This shows the height of the blockchain and a few other bits, including the number of incoming and outgoing connections.

Another neat command is `print_net_stats` which lets us see how much data has been received and contributed to the network and at what rate.

Of course no internet connection is the same and you may want to limit your traffic. You can do so on the fly or by editing the config file we set up earlier. 
It may take some time for you to find the settings that really suit you. 

If you're interested in seeing what else you can do whilst the daemon is running type `help`.

As the initial sync is complete, I'm going to limit my traffic. I'm going to offer 1 MB/s to my incoming connections and 1.5MB/s to outgoing as I use my PC for many other things. I'm going to do so using the commands `limit_up` and `limit_down`.

Once again, please take a look at [MoneroDocs](https://monerodocs.org/interacting/monerod-reference/#commands) for more documentation. It has lots of useful information and will help you to tune your node!


### OUTRO

Well, there we have it, our very own node!

Now we can rest easy knowing that we're supporting the network and have the basis for all our future monero needs!

If you have any comments or questions, feel free to leave them below, but please search for similar questions before doing so.

That's it for this video, if you're interested in seeing how you can put your node to use, you can check out the other videos in this series.

Thanks for watching and bye for now.
