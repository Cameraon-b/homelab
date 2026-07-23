# AETHER Log #38 – Iris, the Rainbow Bridge

**Date: July 22, 2026**

The previous stage of AETHER began with an unsuccessful attempt to turn a Raspberry Pi into a dedicated Kali Linux workstation.

The idea was sensible, but the hardware was not suited to the intended workload. Kali technically ran, yet every interaction felt slow enough that the machine would have become something I avoided rather than something useful. Instead of forcing the original plan, Kali moved to a virtual machine on Cass and inherited the name Pan.

That left the Raspberry Pi without a clear identity.

It had entered AETHER as a possible security workstation, failed in that role, and temporarily seemed like another experiment that had reached its natural limit.

Instead, the Pi was about to become something much more important.

It would become the doorway into AETHER from the outside world.

## Finding a New Purpose for the Pi

The Raspberry Pi did not have enough processing power to provide a comfortable interactive Kali environment.

That did not mean it lacked value.

The mistake had been evaluating it as though it needed to behave like a desktop computer. The Pi did not need to run a heavy graphical operating system, support security tools interactively, or compete with the more capable systems already inside AETHER.

It needed a role appropriate to its strengths:

- Low power consumption
- Quiet operation
- Continuous availability
- A small physical footprint
- Enough performance for lightweight network services
- The ability to remain online without occupying Nora or Cass

FreedomBox had already been installed during the earlier experiment.

Rather than removing it, I began evaluating what the Pi could provide as a small dedicated infrastructure appliance.

One possibility stood out immediately:

A virtual private network.

The goal was to create a secure path into AETHER from outside the apartment.

Instead of exposing BookStack, Memos, Uptime Kuma, SSH, or other internal services directly to the public internet, the Raspberry Pi could accept one carefully controlled WireGuard connection and provide access to the private network behind it.

The Pi would not need to host the applications.

It would simply provide the road leading to them.

## A Different Meaning of VPN

Before this project, I primarily understood VPNs through their consumer use.

Commercial VPN services are commonly presented as tools for hiding a public IP address, encrypting browser traffic, appearing to connect from another geographic location, or preventing an internet service provider from seeing the final destination of a connection.

That is one use of a VPN.

It is not the only one.

Inside infrastructure and enterprise environments, a VPN can be used to extend a private network securely across the public internet.

The objective is not necessarily to hide from the internet.

The objective is to travel through it safely.

With WireGuard configured correctly, a phone using cellular service could create an encrypted tunnel to the Raspberry Pi. Traffic intended for the AETHER network would enter that tunnel, cross the public internet, arrive at the Pi, and then be routed onto the home LAN.

From the perspective of the internal services, the remote device would behave like another authorized network client.

Distance would become largely irrelevant.

## Building the WireGuard Server

FreedomBox provided an interface for configuring WireGuard.

A WireGuard server configuration was created on the Raspberry Pi, followed by a client configuration for my phone.

The initial configuration included the expected components:

- A WireGuard interface on the Pi
- A private and public key pair for the server
- A client key pair
- An assigned VPN address
- A listening UDP port
- A peer entry for the phone
- A public endpoint pointing toward the home internet connection
- A router port-forwarding rule sending WireGuard traffic to the Pi

The router was configured to forward the selected UDP port to the Raspberry Pi.

The client profile was imported onto the phone.

At that point, the design appeared complete.

The phone should have contacted the home router, the router should have forwarded the packet to FreedomBox, and WireGuard should have established the encrypted tunnel.

Instead, the connection did not behave as expected.

## The Stale Handshake

WireGuard showed evidence of a handshake, but it was not current.

The timestamp remained stale.

This created an awkward diagnostic state.

The configuration was close enough that the client and server had apparently communicated at some point, but the tunnel was not consistently establishing a fresh session.

Several possibilities had to be considered:

- The router might not be forwarding the UDP port correctly.
- The endpoint address might be wrong.
- FreedomBox might not be listening on the expected interface.
- The phone might be using an outdated configuration.
- The server and client keys might not match.
- The tunnel might exist but fail to route traffic afterward.
- Firewall rules might allow the handshake but block forwarded packets.
- NAT might not be configured for return traffic.

The WireGuard status was checked repeatedly.

The server interface existed.

The expected port was listening.

The peer was present.

The configuration appeared structurally valid.

Yet the handshake timestamp was not updating.

## Testing the Connection From the Wrong Network

The breakthrough came from a detail so simple that it had been easy to overlook.

The phone was still connected to the home Wi-Fi network.

I had been attempting to test remote access while the supposed remote device was still physically inside the same LAN.

That did not accurately test the path the VPN had been designed to provide.

Wi-Fi was disabled.

The phone switched to cellular service.

WireGuard was activated again.

The handshake immediately became current.

The client was now reaching the Raspberry Pi from the outside world exactly as intended.

The tunnel existed.

The public endpoint worked.

The router was forwarding the port.

FreedomBox was receiving the connection.

The cryptographic relationship between the server and client was valid.

That was the first major success.

It was not yet the final one.

## A Tunnel Without Useful Traffic

Although the handshake now worked, establishing a WireGuard session did not automatically guarantee that the phone could reach the rest of AETHER.

The encrypted tunnel connected the phone to the Pi.

The Pi still needed to forward packets from the WireGuard interface onto the LAN and ensure that replies could find their way back.

IP forwarding was checked:

```bash
sysctl net.ipv4.ip_forward
```

The result confirmed:

```text
net.ipv4.ip_forward = 1
```

Linux was permitted to route packets between interfaces.

The firewall and NAT rules were then inspected.

The investigation included:

- Reviewing `iptables` forwarding rules
- Inspecting packet counters
- Checking the NAT table
- Confirming traffic arrived through the WireGuard interface
- Verifying that packets were allowed toward the LAN
- Looking for evidence that responses were being translated and returned correctly

At one point, packet counters showed traffic arriving from the VPN client but not producing useful return traffic.

This narrowed the problem.

WireGuard itself was no longer the primary issue.

The problem existed in the path beyond the tunnel.

The phone could reach the Pi.

The Pi needed to carry the traffic the rest of the way into AETHER.

## A Serious Key-Management Mistake

During the troubleshooting process, the WireGuard server configuration was examined closely.

While sharing configuration details for analysis, I accidentally exposed the server’s private key in the conversation.

A WireGuard private key is not merely another configuration value.

It is the secret cryptographic identity of the server.

Once disclosed, it must be treated as compromised.

Even though the exposure was accidental and occurred during troubleshooting, there was no responsible way to continue using the same server identity.

The server keys needed to be rotated.

The client configuration also needed to be recreated so that no part of the new tunnel depended on the compromised material.

This turned an already difficult troubleshooting session into a complete rebuild.

It was frustrating, but it also introduced an important operational lesson:

Secrets cannot be treated like ordinary diagnostic output.

Private keys, passwords, API tokens, recovery codes, and authentication certificates must be removed or replaced before sharing configurations.

A working system built on a compromised key is not a successful system.

It is an insecure system that happens to function.

## Rebuilding From the Beginning

The existing WireGuard setup was removed.

A new server configuration was created through FreedomBox.

New server keys were generated.

A new phone client was created.

The new client profile was imported.

The router forwarding configuration was reviewed again.

The tunnel was activated from cellular service.

A fresh handshake appeared.

The new cryptographic relationship worked.

The previous key no longer mattered because it no longer represented the server.

This was more than retrying the same steps.

The rebuild established a clean security boundary after the earlier mistake.

The process now had a verified starting point:

- Fresh server identity
- Fresh client identity
- Known endpoint
- Correct UDP forwarding
- Current handshake
- IP forwarding enabled
- A phone genuinely connecting from outside the LAN

The remaining question was whether the tunnel could finally reach an internal application.

## Uptime Kuma Appears

Uptime Kuma was selected as the first meaningful test.

It was an ideal target.

Kuma was already running internally and provided a simple visual confirmation. If its login page appeared, then the phone was not merely exchanging WireGuard handshakes with the Pi.

It was reaching through the Pi and communicating with a service elsewhere inside AETHER.

The phone remained on cellular.

WireGuard remained active.

The internal Kuma address was opened.

The login page appeared.

That page represented the entire route working from end to end:

```text
Phone on cellular
        │
        │ Encrypted WireGuard tunnel
        ▼
Home router
        │
        │ UDP port forwarding
        ▼
FreedomBox on Raspberry Pi
        │
        │ IP forwarding and routing
        ▼
AETHER LAN
        │
        ▼
Uptime Kuma
```

The certificate warning shown by FreedomBox was expected and unrelated to the WireGuard connection itself.

The important result was that an internal service, unavailable directly from the public internet, was now accessible securely from a phone using cellular data.

Remote access to AETHER was operational.

## Discovering That Mira Had Been Writing

While testing internal services through the VPN, another unexpected discovery appeared.

Memos contained nightly journal entries from Mira.

A cron job configured earlier had quietly continued operating even after I had largely forgotten about it.

Mira had been writing in the background.

The automation had survived.

The schedule had continued running.

The entries had accumulated without requiring attention.

This was memorable because it showed another stage in AETHER’s evolution.

The systems were no longer only alive while I was actively typing commands into them.

Some of them were maintaining routines independently.

The VPN did not create that automation.

It made the results visible from outside the network.

For the first time, I could stand elsewhere, connect securely to AETHER, and discover what its systems had been doing while I was away.

## WireGuard Is Not Limited to the Browser

After reaching Kuma, another realization followed.

WireGuard was not sitting only in front of a web browser.

It had created a network interface on the phone.

Any application whose traffic matched the routes in the WireGuard configuration could use the tunnel.

The applications did not need special WireGuard integration.

The phone’s operating system handled the routing.

A browser could access Kuma.

Termius could use SSH.

A remote-desktop application could potentially reach a Windows machine.

Other internal TCP or UDP services could be accessed according to the same principle.

This led to the next test.

## SSH From a Phone Over Cellular

Termius was opened on the phone.

A host entry was created for Nora using its private AETHER address.

The phone remained disconnected from Wi-Fi.

WireGuard remained active over cellular.

The SSH connection was initiated.

Nora accepted it.

A shell appeared.

Commands typed into the phone were now executing on the Ubuntu server sitting inside the apartment.

This was not remote screen sharing.

It was not a third-party relay service.

It was not a cloud-hosted machine.

The phone had formed an encrypted tunnel through the public internet, entered the private home network through the Raspberry Pi, contacted Nora directly over SSH, and opened an authenticated shell.

I could now administer AETHER from nearly anywhere with cellular or internet access.

The command prompt made the achievement feel real in a way that the WireGuard status screen alone could not.

The VPN was no longer an abstract network service.

It was usable infrastructure.

## Distance Becomes Irrelevant

The most important conceptual lesson from the project was simple:

A properly configured VPN makes physical distance largely irrelevant to the applications behind it.

Nora did not need to understand that the SSH client was miles away.

Uptime Kuma did not need to know that the browser was using cellular service.

Memos did not need to distinguish between a phone sitting inside the apartment and a phone connected through WireGuard from somewhere else.

The tunnel extended the private network.

From the applications’ perspective, the remote client was simply another routed host.

That changed the way I understood VPN technology.

The consumer model says:

> Send my internet traffic through someone else’s server.

The infrastructure model says:

> Extend this trusted private network to where I am now.

I was not using the VPN to escape AETHER.

I was using it to carry AETHER with me.

## The Raspberry Pi Finally Makes Sense

The Raspberry Pi had initially felt like a novelty.

It was amusing because of its size.

It was interesting because it was inexpensive.

It appeared useful in theory, but the failed Kali installation had made its limitations obvious.

As a workstation, it was disappointing.

As a secure, low-power gateway operating continuously at the edge of AETHER, it was nearly perfect.

The Pi did not need to be powerful.

It needed to be dependable.

It could sit quietly, consume little electricity, accept encrypted WireGuard connections, and pass authorized traffic into the rest of the environment.

That humble role gave it more practical importance than the original Kali plan ever would have.

The smallest computer in AETHER became the entrance to everything else.

## Naming the Gateway

The Raspberry Pi could no longer remain Pan.

Pan was now the Kali virtual machine running on Cass.

The Pi needed a new name reflecting its actual role.

Several possibilities were considered.

Charon was appealing because of his role as a ferryman carrying travelers between worlds. The symbolism fit packet routing across the boundary between the public internet and the private network.

The name, however, felt slightly too heavy and too long for such a small machine.

Iris fit better.

In Greek mythology, Iris is a messenger who travels between the divine and human realms. She is associated with communication, travel between worlds, and the rainbow that bridges heaven and earth.

That symbolism mapped naturally onto the Pi.

AETHER could be imagined as the humble human realm.

The public internet existed above it like the heavens: distant, immense, and otherwise separated.

Iris carried messages between them.

The Raspberry Pi did not rule the network.

It did not host its most powerful services.

It quietly connected one realm to another.

The system received its final identity:

**Iris**

Also known as:

**Iris, the Rainbow Bridge**

## The Path Through Iris

The new architecture can be represented as:

```text
The Outside World
Public Internet / Cellular Network
                │
                │ Encrypted WireGuard tunnel
                ▼
       Iris, the Rainbow Bridge
          Raspberry Pi / FreedomBox
                │
                │ Trusted access into AETHER
                ▼
          The Human Realm
              AETHER.LAB
                │
        ┌───────┼────────┐
        │       │        │
      Nora     Cass     WIN-DC01
        │       │
     Docker    Pan
        │
  Kuma / Memos / BookStack / Nexus
```

The name is more than decoration.

It describes the function.

Every remote command passes across the bridge.

Every internal webpage opened from outside follows the same path.

Every SSH session from the phone enters AETHER through Iris.

## A System That Can Be Operated From Anywhere

With WireGuard and SSH functioning, several new operational possibilities now exist.

From a phone outside the apartment, I can:

- Check Uptime Kuma
- Read Memos
- Access internal web services
- Connect to Nora through SSH
- Inspect running Docker containers
- Review disk space and system load
- Restart a failed service
- Read logs
- Verify whether a host is reachable
- Potentially connect to additional machines as remote access is configured

A future incident could look like this:

Kuma reports that BookStack is unavailable.

I connect WireGuard.

I open Termius.

I SSH into Nora.

```bash
docker ps
docker logs bookstack
docker restart bookstack
```

I refresh Kuma.

The service returns to green.

The repair occurs without being physically present.

That is a meaningful change in AETHER’s capabilities.

## Security Boundaries

The new access also introduces responsibility.

WireGuard provides a secure tunnel, but that tunnel leads to sensitive systems.

Several security practices now matter more than they did before:

- WireGuard private keys must remain private.
- Lost or retired client devices should have their peers removed.
- SSH should eventually use key-based authentication rather than relying only on passwords.
- Administrative access should be limited to the systems and accounts that require it.
- The Raspberry Pi and FreedomBox should receive updates.
- Router port forwarding should expose only the WireGuard UDP port.
- Internal applications should not be made public merely because remote access is convenient.
- Configuration backups should exclude or carefully protect private keys.
- Logs should be reviewed if unusual handshakes or access attempts appear.

The accidental key exposure was an early reminder that secure infrastructure depends as much on operational discipline as technical configuration.

The response was correct:

Do not rationalize the exposure.

Rotate the key.

Rebuild the trust relationship.

Continue from a known-secure state.

## Troubleshooting as Layered Isolation

Like the Pan domain-join project, this problem did not have one single failure.

It involved multiple layers:

- FreedomBox configuration
- WireGuard identities
- Client routes
- Public endpoint addressing
- Router port forwarding
- Cellular versus Wi-Fi testing
- UDP reachability
- Handshake verification
- Linux IP forwarding
- Firewall forwarding
- NAT
- Internal service accessibility
- Secret management
- Client reconfiguration after key rotation
- Application-layer testing
- SSH authentication

The only workable approach was to test one layer at a time.

First:

Does the WireGuard interface exist?

Then:

Is the port listening?

Then:

Can the client reach the public endpoint?

Then:

Does the router forward the packet?

Then:

Does the server show a fresh handshake?

Then:

Is the test actually occurring from outside the LAN?

Then:

Can the Pi forward packets?

Then:

Can an internal application respond?

Then:

Can a non-browser application use the same tunnel?

Each successful test reduced uncertainty.

The stale handshake initially suggested a network or configuration failure.

Switching the phone from Wi-Fi to cellular revealed that the test conditions themselves were flawed.

A current handshake proved the public path worked.

Kuma proved LAN routing worked.

SSH proved WireGuard provided general network access rather than access to only one web service.

The project progressed by turning a large ambiguous problem into a sequence of smaller questions.

## Infrastructure Evolves Again

The previous log concluded that AETHER often evolves through constraints.

A problem exposes an opportunity.

A workaround becomes an architectural improvement.

A failed plan becomes a better design.

Iris is another example.

The Raspberry Pi failed as a Kali workstation.

That failure freed Pan to become a more capable VM on Cass.

The abandoned Pi then became available for FreedomBox.

FreedomBox led to WireGuard.

WireGuard created secure remote access.

Remote access revealed Mira’s continuing journal automation.

SSH transformed the VPN from an interesting network experiment into a practical administrative tool.

The Pi’s greatest contribution emerged only after its original purpose failed.

## Final State

At the end of the session:

- The Raspberry Pi runs FreedomBox.
- WireGuard is configured with newly rotated keys.
- The home router forwards the WireGuard UDP port to the Pi.
- A phone can establish a current handshake over cellular.
- The Pi forwards authorized VPN traffic into the AETHER LAN.
- Uptime Kuma is accessible remotely.
- Internal Memos entries can be viewed through the tunnel.
- Termius can SSH into Nora from the phone over cellular.
- Internal services remain private rather than directly exposed.
- The Raspberry Pi has been renamed Iris.
- Iris has received the title **The Rainbow Bridge**.

The defining moment of the evening was not a single command.

It was opening Termius from a phone using cellular data and seeing Nora respond.

That shell represented an encrypted path across the public internet, through a Raspberry Pi, and into infrastructure built piece by piece over the previous months.

The Raspberry Pi no longer feels like a funny little computer.

It is the secure threshold of AETHER.

It is a quiet messenger between worlds.

It is the smallest machine in the environment, yet every remote journey into the network now begins with it.

**Iris stands at the edge of AETHER.**

**The Rainbow Bridge is open.**
