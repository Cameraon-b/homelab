# AETHER Log #46 – Hermes Reaches Nora

**Date:** November 23, 2026  
**Period covered:** November 21–23, 2026

The last log ended with a plan to let Hermes deploy a Nexus preview to Nora. This week I tested the part that crosses machines. I signed in to Nora over SSH using a key for Hermes's dedicated account, started its rootless Docker daemon, and got `Hello from Docker!` back. The Nexus preview still has a few steps to go, but the deployment account now works.

## Reeba Goes Wired

I moved Reeba from Wi‑Fi to Ethernet, turned off Wi‑Fi, and checked that RustDesk and Minecraft still worked. I nearly closed the GLPI ticket before trying the internal AETHER sites in a browser. That turned up one more problem. Reeba could get onto the network, but it couldn't resolve some of the names I use for services on Nora.

Reeba, Cass, and Grayson's computer are outside the AETHER domain, and I had been relying on local hosts-file entries for those names. Comparing Reeba with Cass reminded me where I'd already handled it. I restored the entries on Reeba, tested the sites again, and confirmed they loaded over Ethernet. I'm glad I left the ticket open long enough to test the browser.

I also recovered the Iris administration login. I'd forgotten which username I'd used and found it in my browser history. WireGuard was already working throughout that little detour.

## Giving the Network an Inventory

I picked **Orion** for the router. **Janus** is the switch and **Iris** is the FreedomBox that handles the VPN. I started a quick-reference spreadsheet for device IPs, MAC addresses, operating systems, and services. BookStack still has the longer notes. I wanted one place where I could quickly look up a device or identify it by its MAC address.

The Ethernet swap also got me thinking about how much gear and cabling has accumulated around the desks. Grayson and I are talking about taking a day or two during our December break to rearrange the setups and redo the cabling. I also put KeePass on the list, with separate databases planned for personal and AETHER credentials.

## Terminal Assistants on Nora and Pan

I wanted two Termius sessions into Nora. One is my working shell, and the other is where I can ask a question and paste the output I'm looking at. I installed Pi on Nora and connected it to a hosted model. That let me use the terminal interface without asking Nora's CPU to run the model alongside Docker and KVM.

I set up the same workflow on **Pan**, the Kali Linux VM. Pi's installer stalled during the APT step there, so I installed Node through `nvm` and Pi through npm. The first attempt to load `nvm` missed because it had installed under `~/.config/nvm`. Sourcing it from that directory got the rest of the install working.

On both machines, I launched Pi with model tools and automatic project context disabled. I run the commands in my own shell and paste the output I want Pi to explain. That's the setup I wanted for learning my way around both machines while I'm using them.

## Nexus Messaging and Sprint Closeout

Sprint 6 proved that Mira could reach the Nexus API and submit a message using her agent token. She also appeared as an agent in the Common Room participant list. The message reached the approval queue, where it stayed because I didn't yet have a way to approve it in Nexus. That was enough to show that the API could accept a message from an agent running in its own harness.

I set Hermes and Pi on Sprint 7 to work through human-to-agent and agent-to-human messaging, including the message approval flow. I still need to verify a full exchange from inside Nexus. Agent-to-agent messaging and event-driven delivery are later work. I've been seeing roughly 10–15% of my OpenAI allowance used per sprint with the Hermes–Pi workflow, which makes it more practical to run sprints regularly.

I also tested giving Hermes access to our Gitea instance. It successfully pushed a copy of Nexus there. For future sprint closeouts, I want Hermes to write an explanation with references to the code and save the corresponding repo state to Gitea after my approval. I still handle pushes to GitHub. The explanations give me a way to follow what Hermes and Pi changed and learn how those parts of Nexus work.

## Sprint 9 – A Deployment Account on Nora

I created a dedicated SSH account for Hermes and installed its public key. Nora already had Docker CE and the rootless setup tools. The installer stopped on a missing `uidmap` dependency, so I installed that through my admin account and retried from the Hermes session.

The rootless daemon came up under Hermes's account. Docker reported `name=rootless`, and the test container ran successfully. I also tried to list containers against Nora's shared Docker socket from the Hermes session and got `permission denied`. Those two checks tell me Hermes can run containers in its own environment while the containers that already serve AETHER stay under the system daemon.

The next step is to bring up the Nexus Compose stack under `/srv/nexus` and verify its health from Nora. Nginx Proxy Manager owns ports 80 and 443, so I'll check the existing `nexus.aether.lab` upstream and verify that the proxy can reach the new backend before I switch the route. I'm handling the proxy and TLS changes myself. The goal is still to open the preview over WireGuard and try it from my phone before approving a release.

Nora also has pending updates and a reboot notice. My backups are a little dated, so I decided to do a fresh backup and handle the reboot and updates when I'm off work and have time to check the services afterward.

## Final State

| Area | Status as of November 23 |
| --- | --- |
| Reeba | Ethernet active, Wi‑Fi disabled, and RustDesk, Minecraft, and internal name resolution verified |
| Iris and inventory | FreedomBox admin access recovered. Orion named and the device spreadsheet started |
| Nora and Pan | Pi working in both terminals for interactive help |
| Nexus messaging | Mira registered and submitted a message. Approval blocked delivery in Sprint 6. Sprint 7 was started to address the approval flow and two-way messaging |
| Gitea | Hermes successfully pushed a Nexus copy. Future pushes and sprint explanations are part of the approval workflow |
| Hermes on Nora | SSH and rootless Docker verified with a running test container. Access to the shared Docker socket was denied |
| Nexus preview | Compose deployment, health check, and proxy cutover still to come |
| Nora maintenance | Fresh backup, reboot, and updates deferred until time off |

## Closing Thoughts

A few days ago, the main experiment was whether Hermes could hand work to Pi and review it. Now I've tested another part of the workflow. An agent on Reeba can have its own identity on Nora and a place to run the software it helped build. I can see where each part lives, which account is doing the work, and where I want to make the final change myself.

The next milestone will be opening Nexus from my phone and trying a build that Hermes brought up on Nora. I still want that first conversation with Mira inside Nexus, too. Then I can review the deployment and talk to the agents from the same place.
