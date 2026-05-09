*Initial Validation*

-Network Verification
  Command executed:
    ip addr
    
-Observations
  Active Ethernet interface detected:
    enp2s0

  DHCP-assigned IP address:
    192.168.1.71/24

  Broadcast address:
    192.168.1.255

-Interpretation
  Host successfully connected to local network via Ethernet.

-Hardware Validation
  Commands executed:
    free -h
    lscpu
    lsblk
    lspci
    sudo dmidecode -t system
    sudo dmidecode -t baseboard
    sudo dmidecode -t memory
    
-Observations
  Host recognized all installed memory.
  1TB disk detected.
  Optical drive detected as:
    /dev/sr0

  Successfully tested optical drive with:
    sudo eject /dev/sr0
    
  Note
    Linux Server automatically recognized optical hardware without additional driver installation.

-Virtualization Validation
  Command executed:
    lscpu | grep Virtualization
  
-Result
  AMD-V

-Interpretation
  Hardware virtualization support confirmed.
  Host is suitable for KVM.

-Hypervisor Installation
  Initial Issue
  Attempted installation using deprecated package names.
  Package manager returned:
    Unable to locate package

-Troubleshooting
  Updated package cache:
    sudo apt update
  Adjusted package names based on repository suggestions.

-Installation Command:
  sudo apt install qemu-system-x86 libvirt-daemon libvirt-clients virtinst bridge-utils -y
  
-Validation
  Service Status
  Command:
    sudo systemctl status libvirtd
    
-Result
  active (running)

-VM Inventory
  Command:
    sudo virsh list --all
    
-Result
  Empty inventory returned successfully.

-Interpretation
  Host is now functioning as a virtualization server.

-Lessons Learned
  Physical indicators (LED activity, keyboard responsiveness) help validate system state during installs.
  Package names may change across Linux releases; package manager suggestions should be reviewed carefully.
  Hardware capabilities can be validated entirely through CLI tools.
  Linux command output is often paged; learned navigation using less (space, b, q).
  
-Next Steps
  Create Windows Server virtual machine.
  Configure networking for guest systems.
  Begin learning Active Directory.
