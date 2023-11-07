### High Availability (HA) **🏷️**

**TL;DR**

-   Goal: **Maximizing** a **system's uptime** 📈.
-   **User disruption is acceptable** ✅.
-   **More** **budget** friendly **🏷️**
-   With **Spare infrastructure ready** to **switch to you can minimize outages** 👌.
-   **cope** through **disaster.**
-   **e.g. 4x4 repearing a tire hole with a spare tire**
    -   spare tire.
    -   some **user disruption** while doing so.

### Fault-Tolerance (FT) 💰

^6c176e

-   **Goal**: 
	- **Work** _**through failure**_ of some its **components** 🩹  
	- ****************************minimize outages**************************** ⚡.
-   **User disruption** **not allowed** or acceptable 🚫.
-   **More** expensive 💸.
-   _**Outages** must be **minimized** and the **system needs** levels of **redundancy**_.
-   **Mission** or **life critical** situations 🔫
-   **operate** through **disaster.**
-   **e.g. Resilent systems on large planes**
    -   (like extra **engines** than it needs to so it can operate **through  failure**)

### Disaster Recovery (DR) ☠️

-   what to plan for ? and **do** when **disaster occurs** ?
-   ********e.g.******** **DR Process** are pilot or passanger **ejection systems.**
-   **Goal**: DR is a **process** designed to keep the **non replaceable** parts **safe.**
-   Set of **policies**, **tools** and procedures to **enable the recovery** or **continuation** of **vital** technology infrastructure and systems **following a natural** 🍃 **or human-induced disaster** 🤡.
-   **DR** can largely be **automated** to eliminate the **time** for **recovery** and **errors**.

This involves:

-   **Pre-planning**
    -   Ensure **plans** are in place for **extra hardware**
    -   **\[DO NOT STORE\]** **backups** at the **same site** as the **system.**
-   **DR Processes**
    -   **Cloud machines** **ready** when **needed.**
    -   Run **periodic** _**DR Testing**_.
    -   all the **process** and **tools** should be **properly documented**.
        -   all the **parties** involved should run periodic **DR Testing** from time to time to minimize **human error**.
        -   all **logins to key systems** need to be available for staff at time of disaster.
-   This is designed to keep the crucial and non replaceable parts of the system in place.
-   _**Used** when **HA** and **FT** don't work._

![[Pasted image 20230521131034.png]]