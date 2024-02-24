
--- start-multi-column: ExampleRegion1  
```column-settings  
number of columns: 2  
largest column: auto  
```

## (NGW) NAT Gateway
- must be in **public subnet**
- Elastic **IP Required**
- Fixed to one AZ
- optional, just required for private subnets
- Handled by **AWS** , no administration overload.
- Don't support port forwarder.    
- No support for **IPv6**.


--- end-column ---

## Nat Instance
- Manage by user.
- Use as Bastion server.
- Support port forwarding.
- In order to specify as **Target** in a route **table**, Must disable Source and Destination.
- No support for **IPv6**.

--- end-multi-column
