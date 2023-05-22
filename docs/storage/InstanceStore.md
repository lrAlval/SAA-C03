 # EC2 Instance Store

- **hardware disk**, **lower latency** than [[EBS]]
- better **IO** performance
- **Backup** and **Replication** are **customer responsability**

## Caveats
- **Data will** be **lost** if instance is stopped (ephemeral)
- Risk of **data loss** if hardware **fails**

## use case
- Good for **buffer**, cache **,** scratch data, temporary content.
