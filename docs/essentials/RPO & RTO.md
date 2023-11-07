## TL;DR
-   Recovery Point Objective (**RPO**) ⇒ (think of **max** acceptable data loss) - **max** amount of data (**time**) that **can be lost.**
-   Recovery Time Objective (**RTO**) ⇒(**max** acceptable time can **recover operational state**) **max** tolerable **duration** of a service **outage**.
- Aim for **Goldilocks** .. As close to the **TRUE** business requirements as possible.

# Recovery Point Objective (RPO)

-   **max** amount of data (**time**) that **can be lost.**
-   **Lower RPO** = **More** **Frequent Backups = Expensive Budget \$\$\$ 💰
-   **Higher RPO** = **Less** Frequent Backups **= Lower Budget \$\$\$ 💰
-   each back up = Recovery Point (**RP**) ⇒ can either be **full recovery back up** or **incremental backup**.
-   **Best Practice** it is recommended that a backup_frequency is ≥ desired (RPO)
    -   e.g RPO = 6 hours , back_up frequency should be every 6 hours or 3 hours to avoid data loss
    -   tradeoff ⇒ with more frequently back ups every x hour / minute:
        -   we **minimize** the loss of **data** but we increase the **cost** \$\$\$


# Recovery Time Objective (RTO)

-   Max tolerable length of time a system can be **down after a failure or disaster occurs.**
-   Max **tolerable time** it takes for a **system** to **recover** and **resume operations.**
-   **Maximum time from when a failure occurs through to when the business will need that system back up and running in an operational state.**

### Can be reduced via
-   careful planning.
-   monitoring.
-   notification process.
-   spare hardware.
-   trainings.
-   more efficient systems (**Virtual Machines** or **AWS**).