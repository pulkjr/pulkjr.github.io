---
authors:
  [pulk]
---
# I Start Using Ansible AAP

I've been dreading this day. I'm primarily a PowerShell person. I have been using it since v1 was released and love 
the ease of use it provides to write quick scripts. If I need more speed I switch over to c#. I've used DSC but don't
currently have a customer willing to go all in on it.

The main problem I have heard from people is that DSC doesn't have the GUI tools that people want when interacting 
with automation. So here I am with an approved fully deployed AAP Instance and the requests from peers and managment to
start automating with it. So what do I do? 

Your right! I spend the next 6 months finding every excuse I can find, not to use it, but now I have a problem that is
not necessarily easier with PowerShell. I need to automate Brocade. Brocade has done most of the work already. So at 
the start of the month I began using Ansible.

##  Learning

I figure the best place is to start with the RedHat curriculum for Ansible, that shoud give me what I need to start.
I've been listening to the AAP administators war stories and have a fairly good idea of the concepts so the training isn't
revolutionary. The problem is that everything is geared toward running it locally. So about half way through the training
I decide to stop and try doing a basic login and collect information.

## First AAP Playbook

My first playbook is to collect facts from the Brocade switch. This should be straight forward plug in a couple things
and wallah. Nope. All the training is around running ansible on the platform you are configuring. In the case of a Brocade
switch you need to run it on **Localhost** then pass the target from the inventory into the play.

I spend then next couple hours trying to get this to work. None of the errors make sense. Most of them are syntax errors
or a cryptic Python error. Now I'm reading through Brocades Python code trying to figure out why it will not connect.
I start trying to run it locally on my machine. Doesn't work more errors but I can make changes to the Python and finally
figure out that there is an SSL error on the switch. Try a different switch and wallah it works. Cue palm face. I learned
a crep load though about how the connection works between the Ansible container and the Brocade switch.

## Second Playbook

I'm more comfortable with the process now so I attempt to make some changes. I need to make accounts on the switch and 
the [Rest API](https://docs.broadcom.com/doc/FOS-82X-REST-API-RM) shows that there is an endpoint for userconfig. Also 
the [Brocade FOS Collection](https://galaxy.ansible.com/ui/repo/published/brocade/fos/content/module/brocade_security_user_config/) has a module for it. Seems safe enough. I follow the guide and it works first try. Alright that was the dopamine hit
that I needed! Everythings gonna be Ansible!

Accounts created on the switch but I need to make this a MFA account using the user public key. I read through the REST API doc to find the endpoint but am unable to find one for this. There is though a [SSH Module Brocade wrote](https://github.com/chipcopper/ansible-fos-command) that provides an expect style interaction with Brocade. This fails misserably. I end up [forking the repo](https://github.com/pulkjr/ansible-fos-command) because there is a bug when running from a FIPS enable RedHat system that doesn't allow MD5. I [found a fix](https://stackoverflow.com/questions/67559170/paramiko-ssh-command-execution-failing-with-valueerror-digital-envelope-routi) and updated the code.

I can now execute commands with SSH against Brocade. My resources suck though and the method used to find the prompt destorys the next day and a half. I've never written in Python so I'm having to stuggle though the code and debug. I finally figure out that I need to greatly increase the timeout for the initial connection to the switch. From there I update the code to use a regex expression to look up the prompt. This increases that stability on the slow connection. Finally I update the connection variable to meet the other modules within the Brocade.FOS Collection. I'm back in business!
