---
title: From Zero to Self-Hosted Building My First Homelab Architecture
date: 2026-05-29 22:00:00 +0200
tags: []     # TAG names should always be lowercase
---

If you had told me a year ago that I would be managing a multi-node home server infrastructure, I wouldn't have believed you. When I started out, I began at absolute zero. I didn't know what a hypervisor was, Docker was just a tech buzzword, and my understanding of DNS was completely non-existent.

My entry point into this world was simple: a single Raspberry Pi dedicated to running Home Assistant. It was a fantastic way to dip my toes in, but as I expanded my smart home and added more integrations, the Pi hit its hardware limits. I installed way too many add-ons, bogged down the system resources, and eventually, it crashed.

Around the same time, I hit a completely different digital wall: my Google Photos storage limit. I refused to pay a recurring monthly fee just to store my own files and memories. The idea of truly owning my data by de-Googling my life became the ultimate goal. What started as a practical workaround for cloud storage limits quickly evolved into a genuine passion for self-hosting, networking, and systems administration.

Here is a breakdown of the entire infrastructure built from scratch, along with a deep reflection on every service running in the lab today.

[Click to open interactive architecture diagram](https://excalidraw.com/#json=1OqsmmwloA736Fmd9TeWH,TqMcaSLIY9npygPiMjhGbQ)

---

### The Hardware Ecosystem: Resourceful and Repurposed

You do not need to spend thousands of dollars on enterprise rack-mounted gear to get started. This entire setup is built from budget-friendly, repurposed hardware that has been systematically upgraded over time.

* **Node 1 (The Main Server):** A repurposed school PC featuring an AMD A8-7600 processor with 4 cores. Because the barebones PC itself was free, the budget went entirely into upgrades. It was opened up, maxed out with 16GB of DDR3 RAM, and configured with two 1TB hard drives for direct storage.


* **Node 2 (The Smart Hub & DNS):** The original Raspberry Pi, equipped with 4GB of RAM. Instead of forcing it to do everything, its role is now highly focused. It runs Home Assistant OS off a 1TB USB hard drive and actively handles network-wide ad blocking.


* **Nodes 3 & 4 (The Compute Fleet):** Two repurposed Dell Latitude 5420 laptops equipped with Intel Core i3 processors. Node 3 runs bare-metal Ubuntu to manage a 3D printing environment using Klipper, Moonraker, and Mainsail. Node 4 runs Coolify to deploy personal projects alongside a Hermes agent. The absolute best part of using old laptops? The built-in laptop batteries act as a free, automatic hardware UPS, keeping the compute nodes online even if the power blinks.



---

### The Software Architecture: Hypervisors & Containers

Going from a standard desktop user to managing server operating systems was a massive educational leap. Learning how to properly isolate applications completely changed the reliability of the lab.

* **The Hypervisor (Proxmox VE):** Running Proxmox VE directly on the bare metal of the main PC was the first major breakthrough. It taught me how to cleanly divide system resources. It hosts an Ubuntu Server VM dedicated purely to Samba for network file sharing (1 vCPU, 1GB RAM) and a main Docker host VM given the bulk of the power (3 vCPUs, 13.6GB RAM).


* **Containerization (Docker Compose):** Learning Docker Compose changed everything. Instead of installing applications directly onto the host machine and tangling up dependencies, services are deployed and isolated cleanly using simple, text-based configuration files.



---

### Reflection on Every Hosted Service

Every single application running in this environment represents a specific problem solved and a steep learning curve conquered.

#### Data Ownership & Storage

* **Immich:** This is the definitive solution to running out of cloud storage. Setting it up is a masterclass in local database performance, matching the speed, facial recognition, and mobile backup experience of commercial alternatives without data caps or privacy compromises.


* **Nextcloud:** A complete Google Drive and productivity suite replacement. Deploying it teaches you how to manage web server environments, optimize cloud synchronization, and handle large-scale file storage safely.


* **KaraKeep (Formerly Hoarder):** My self-hosted solution for link and bookmark storage. Moving this away from proprietary platforms means all my saved research, technical documentation, and links are kept in a centralized, private repository that I completely control.
* **Bitwarden:** Moving credentials off third-party cloud vaults into a locally hosted instance is a major security milestone. It shifts the complete responsibility of credential security to local hardware, emphasizing the importance of secure container deployments.
* **Samba:** Running this inside a dedicated, lightweight VM inside Proxmox demonstrates the architectural value of keeping data storage separate from the application layer. It provides a clean, zero-fuss way to handle cross-platform file transfers over the local network.



#### Automation & Deployment

* **Home Assistant OS:** The original gateway drug to the entire lab. Isolating it strictly to the Raspberry Pi after its initial overload crash highlights a fundamental system design principle: keeping critical home automation infrastructure independent so it remains stable regardless of experiments on the main server.


* **Coolify & Hermes Agent:** This stack completely transformed standard laptop hardware into a private, PaaS (Platform-as-a-Service) environment. It bridges the gap between raw server administration and modern developer workflows, making it incredibly easy to deploy personal code projects via automated builds.
* **Klipper, Moonraker, & Mainsail:** Running this stack on bare-metal Ubuntu showcases how a homelab can interface directly with physical hardware. It utilizes the laptop's built-in battery as a hardware UPS, preventing ruined 3D prints during minor power fluctuations.



#### Media Automation & Entertainment

* **Jellyfin:** Proved that efficient media streaming is fully achievable on older hardware without massive enterprise overhead. Because of the older AMD A8 CPU constraints, it forces an understanding of media codecs and client-side direct playing to avoid resource-heavy server transcoding.


* **The *Arr Stack & qBittorrent:** The ultimate practical lesson in container interoperability and shared storage volumes. Configuring these services to communicate via APIs and automatically handle file post-processing is a massive milestone for mastering Docker directory structures.



#### Networking, Monitoring, & Security

* **AdGuard DNS:** The bridge into intermediate networking. Running this as an add-on on the Pi teaches how DNS routing functions, giving the entire household network-wide privacy controls and local domain routing without requiring an expensive, enterprise-grade managed router.
* **Cloudflare Tunnels:** The magic bullet for remote access. It completely shifts how edge security is approached by allowing secure incoming traffic to the `magor-lab.hu` domain without exposing open ports to the public internet.


* **Agent DVR:** Handles high-throughput security camera streams locally. It serves as an excellent case study in managing continuous video processing pipelines without overloading the main server VM's CPU allocations.


* **Uptime Kuma:** Taught the value of proactive infrastructure monitoring. Instead of manually checking if a site or service is up, it introduces automated health checks and immediate visibility into network stability.
* **Dozzle:** A massive quality-of-life utility for a containerized lab. It removes the friction of debugging by streaming live Docker container logs directly to a clean web interface, saving constant SSH terminal commands when an app misbehaves.
* **Grafana:** The visual culmination of the lab. It teaches how to collect, aggregate, and parse system metrics, turning raw hardware data into scannable, actionable performance dashboards.

---

### Operational Lessons Learned

Operating on a flat network utilizing a standard ISP router without VLAN support forced a focus on maximizing basic software tools rather than throwing money at expensive networking gear.

The absolute most critical lesson, however, was establishing a resilient backup strategy. Moving past the dangerous "manual Proxmox backups whenever I remember" phase was essential. The entire ecosystem is now secured with automated weekly backups and a strict two-week retention policy, ensuring that when something inevitably breaks during an upgrade, it takes minutes to restore rather than days.

Building this homelab was a massive leap from where it started. Going from knowing absolutely nothing about server administration to successfully running a private cloud infrastructure proves that you don't need a professional background in IT to take control of your own data—you just need a starting point and the willingness to learn.