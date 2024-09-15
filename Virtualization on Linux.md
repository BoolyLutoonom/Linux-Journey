## What is Virtualization ?
Simply put, it is a process that allows for more efficient use of physical computer hardware and is the foundation of cloud computing. 

![[virtualization.png| 350]]

### What is Hypervisors ?
A hypervisor is the software layer that coordinates VMs. It acts as an interface between the VM and the underlying physical hardware, ensuring that each has access to the physical resources it needs to execute. Also ensures that the VMs don't interfere with each other by impinging on each other's memory space or compute cycles.

### Types of Hypervisors
<table>
	<tr>
		<td><b>Type 1 hypervisors</b> (Bare-metal)</td>
		<td> <b>Type 2 hypervisors</b></td>
	</tr>
	<tr> 
		<td>
			<ul>
				<li>These run <b>directly on the computer hardware.</b></li>
				<li> They mange and create virtual machines without needing a regular operating system(OS) first.</li>
			</ul>
		</td>

		<td>
			<ul>
				<li>These run <b>on top of an existing operating system</b>(like Windows or Linux).</li>
				<li>They create and manage virtual machines but need the regular OS to be running first.</li>
			</ul>
		</td>
	</tr>
</table>

## Types of virtualization
<table>
	<tr> 
		<td><b>Desktop virtualization</b>
		</td>
		<td>It lets us run multiple desktop operating systems, each on the same computer. There are two types of desktop virtualization.
			<ul>
				<li><b>Virtual desktop infrastructure (VDI)</b> lets usaccess a virtual desktop environment from any device, where the desktop's software and data are hosted on a central server rather than on your local computer.</li>
				<li><b>Local desktop virtualization</b> allows you to run virtual machines on your own computer, creating and managing multiple virtual desktops and operating systems from your physical machine.</li>
			</u>
		</td>
	</tr>
	<tr>
		<td><b>Network virtualization</b>
		</td>
		<td>Network virtualization uses software to create a simplified, virtual view of a network, allowing administrators to manage and control network elements (like switches and routers) from one central console without needing to handle the physical hardware directly.
			<ul>
				<li><b>Software-Defined Networking (SDN)</b> it virtualizes the hardware easier and more flexible.</li>
				<li><b>Network Function Virtualization (NFV)</b> it virtualizes specific network appliances, like firewalls and load balancers, making them easier to mange.</li>
			</ul>
		</td>
	</tr>
	<tr>
		<td><b>Storage virtualization</b>
		</td>
		<td>Storage virtualization combines all storage devices on a network into one large, easy-to-manage pool, allowing you to allocate storage space to virtual machines as needed and use all available storage more efficiently.
		</td>
	</tr>
	<tr>
		<td><b>Data virtualization</b>
		</td>
		<td>Data virtualization is like a universal translator for data. It creates a software layer that lets applications access and use data from various sources, formats, and locations—whether it's in the cloud, on local servers, or in different file types—without needing to move or combine the data. This helps connect and use data from different places more easily.
		</td>
	</tr>
	<tr>
		<td><b>Application virtualization</b>
		</td>
		<td>Application virtualization lets us use software without installing it directly on our device's operating system. It is further divided into three types.
		<ul>
			<li><b>Local Application Virtualization</b> where the app runs on our device but in a special virtual environment, not directly on our hardware.</li>
			<li><b>Application Streaming</b> where the app is stored on a server, and only the parts we need are sent to the device when we use it.</li>
			<li><b>Server-based Application Virtualization</b> where the app runs entirely on a server, and our device only shows the app's interface.</li>
		</ul>
		</td>
	</tr>
	<tr>
		<td><b>Data center virtualization</b>
		</td>
		<td>Data center virtualization turns a single physical data center into multiple virtual data centers by using software to manage the hardware. This way, different clients can use their own separate virtual data centers on the same physical hardware, making it easy and quick to set up cloud-based computing without buying new hardware.
		</td>
	</tr>
	<tr>
		<td><b>CPU virtualization</b>
		</td>
		<td>CPU virtualization lets one physical CPU act like several separate CPUs, so multiple virtual machines (VMs) can use it at the same time. Initially, this was done with software, but now many CPUs have built-in features to make this process faster and more efficient.
		</td>
	</tr>
	<tr>
		<td><b>GPU virtualization</b>
		</td>
		<td>A GPU is a powerful processor designed to handle complex graphics and calculations. GPU virtualization lets multiple virtual machines (VMs) share the GPU's power to speed up tasks like video processing and AI.
			<ul>
				<li><b>Pass-through GPUs</b> give one VM full access to the GPU.</li>
				<li><b>Shared vGPUs</b> split the GPU's power among several VMs so they can all use a portion of it</li>
			</ul>
		</td>
	</tr>
	<tr>
		<td><b>Linux virtualization</b>
		</td>
		<td>Linux has a built-in tool called <b>Kernel-based Virtual Machine (KVM)</b> that lets you create and run virtual machines (VMs) on your Linux computer. This tool works with Intel and AMD processors to allow multiple virtual computers to run on one physical machine. Because Linux is open source and customizable, you can set up VMs with specific Linux versions or security settings to fit different needs.</td>
	</tr>
	<tr>
		<td><b>Cloud virtualization</b>
		</td>
		<td>Cloud computing relies on virtualization to provide services by using virtual versions of physical resources.
			<ul>
				<li><b>Infrastructure as a Service (IaaS)</b> which offers virtual servers, storage, and network resources that we can set up according to our needs</li>
				<li><b>Platform as a Service (PaaS)</b> which provides virtual development tools and databases to help us build and run applications in the cloud.</li>
				<li><b>Software as a Service (SaaS)</b> which delivers software applications over the internet, so we can use/access them directly without needing to worry about underlying hardware.</li>
			</ul>
		</td>
	</tr>
</table>

## How does KVM work ?
Kernel-based Virtual Machine (KVM) is a technology that allows us to create and run virtual machines on a Linux computer. To use KVM, we need a Linux operating system and a CPU that supports virtualization. Both Intel and AMD processors that use the x86 architecture and have virtualization extensions (Intel VT-x for Intel CPUs and AMD-V for AMD CPUs) are compatible with KVM. This enables efficient management of multiple virtual machines on our system.
### How to check if our CPU supports virtualization extensions ?
#### Check for Intel VT-x or AMD-V Support
Run the commands in terminal:
```bash
grep -E 'vmx' /proc/cpuinfo
```
```bash
grep -E 'svm' /proc/cpuinfo
```
- `grep`: Searches for patterns in text.
- `-E`: Enables extended regular expressions.
- `'vmx'`: This is the flag that indicates Intel VT-x support.
- `svm`: This is the flag that indicates AMD-V support.
- `/proc/cpuinfo`: A file that contains information about the CPU.

If the output includes `vmx`, then the CPU supports Intel VT-x. And, if the output includes `svm`, then the CPU supports AMD-V.
### Check for KVM Support
Run the commands to check if KVM models are loaded or not:
```bash
lsmod | grep kvm
```
- `lsmod`: Lists all the currently loaded kernel modules.
- `grep kvm`: Filters the output to show only lines related to KVM.

If the output includes `kvm_intel` or `kvm_amd` (depending on the CPU), KVM is supported and active.
### Verify KVM Installation
Run the commands to check if KVM is installed and properly configured:
```bash
sudo kvm-ok
```
* `kvm-ok`: Checks if the system supports KVM.

it should give an output similar to this:
```bash
INFO: /dev/kvm exists
KVM acceleration can be used
```
- `/dev/kvm exists`: This confirms that the KVM kernel module is installed and running on your system.
- `KVM acceleration can be used`: This indicates that your system supports KVM and can use it for virtual machine acceleration.

## Checking for virtualization support and troubleshooting
### Troubleshooting BIOS Settings
If the CPU supports virtualization but KVM isn’t working, we may need to enable virtualization in the system’s BIOS/UEFI settings:
1. **Restart the computer** and enter the BIOS/UEFI settings. This is usually done by pressing a key like `F2`, `F10`, `Delete`, or `Esc` during startup (this key varies by manufacturer).
2. **Enable Virtualization**: Look for a setting like “Intel VT-x” or “AMD-V” and ensure it is enabled.
3. **Save and Exit** the BIOS settings, then try the commands again.