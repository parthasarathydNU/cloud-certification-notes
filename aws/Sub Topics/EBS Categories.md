https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html

![[Pasted image 20230928222434.png]]
### General Purpose (SSDs) gp2 / gp3
#exam 

**Cost effective storage for low latency**
- gp3 IOPS and throughput can be set independently
- Volume of 1 GiB upto 16TiB 

gp3: newer generation of volumes
- Baseline of 3,000 IOPS and Throughput of 125 MiB/s
- Can be increased up to 16,000 IOPS and 1000MiB/s of throughput - **independently**

gp2: older version
- Size of the **volume and the IOPS** are **linked to each other**- Max IOPS is 16,000 

### Provisioned IOPS (SSD) PIOPS (io1/ io2)
#exam 

- Applications that need sustained IOPS behavior
- Supports EBS Multi Attach
- **>= 16,000 IOPS**
- I/O critical applications like databases where consistency and performance is key
- Max IOPS is **64,000 IOPS for EC2 Nitro Instances** and 32,000 IOPS for other instances [[Nitro System]]
- Increase IOPS independently of storage size
- io1 - 4GiB - 16 TiB

io2 **Block Express** - 4GiB to 64 TiB volume
- Up to **256,000 IOPS (io2)** with a volume ratio of 1000 IOPS / 1 GiB
- **Sub - milli second latency**


![[Pasted image 20230928222500.png]]
### Hard Disk Drives (HDD) (s throughput - 1/ s cold -1)
- Cannot be boot volumes
- 125 GiB - 16Tib

Throughput optimized st-1
- Big data, data warehousing and log processing applications 
- Max throughput of 500 MiB/s and a max IOPS of 500

Cold HDD sc - 1
- This is for archive data
- Lowest possible cost
- Max throughput 250 MiB/s and IOPS 250 as well

