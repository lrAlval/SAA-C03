 # EC2 Instance Store

- **hardware disk**, **lower latency** than [[EBS]]
- better **IO** performance
- **Backup** and **Replication** are **customer responsibility**

## Caveats
- **Data will** be **lost** if instance is stopped (ephemeral)
- Risk of **data loss** if hardware **fails**

## Use case
- Good for **buffer**, cache,** scratch data, temporary content.
