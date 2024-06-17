https://aws.amazon.com/what-is/block-storage/#:~:text=Block%20storage%20is%20technology%20that,for%20fast%20access%20and%20retrieval.

Block Storage is a technology that controls data storage and storage devices. 
- It directly takes data, splits it into blocks of equal size
- The block storage then takes this data block and stores it on the underlying physical storage 
- in a manner that is optimized for fast access and retrieval

Developers prefer block storage for applications that require fast access and retrieval. File storage has an extra layer of file paths and file names to do before accessing a file.

### Benefits of block storage: 

#### Performance:
- Block storage uses limited metadata but unique identifiers to assigned to each block for write/read operations
- Using reduced metadata reduces the data transfer and allows servers to efficiently access data on blocks
- Since metadata is limited, block storage delivers ultra-low latency DB reads and writes that are key to high performance applications - so EBS is a good root volume to use for applications like a database
- Block storage models allow multiple paths to the underlying data, whereas file system based models allow only one path to the data - through the file directory path and the file name

#### Scalability
- New blocks can be added to EBS to ensure growing capacity needs

#### Frequent Modifications
- Supports frequent data writes without affecting performance
- Instead of modifying the whole file, EBS identifies the particular block to ammend
- This makes EBS a good choice to maintain large files that require frequent updates

#### Data Grouping !
EBS allows data grouping in ways that would reduce resource usage: 
- Frequently modified data can be stored on specific blocks and warm / cold data which are based on static flies can be stored on other blocks
- Further, the blocks with frequent reads and writes can be provisioned an SSD for low latency and the blocks with static data can be based on lower cost hard drivs



