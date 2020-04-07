---
title: "What is Object Storage?"
slug: what-is-object-storage
---

According to Wikipedia, **Object Storage** is described as "a storage architecture that manages data as objects, as opposed to other storage architectures like file systems which manage data as a file hierarchy and block storage which manages data as blocks within sectors and tracks."

Still not very clear isn't it? Let's add some more details!

**Object Storage** is essentially a different way of storing, organizing and accessing data. This kind of platform provides a storage infrastructure to store files with lots of metadata added to them – referred to as objects. With Object Storage, there is no file system hierarchy. Users typically access object storage through applications that uses a REST API (an internet protocol, optimized for online applications). This makes object storage ideal for all online, cloud, environments. When objects are stored, an identifier is created to locate the object in the pool. Applications can very quickly retrieve the right data for the users through the object identifier or by querying the metadata (information about the objects, like the name, when it was created, by who etc.). This approach enables significantly faster access and much less overhead than locating a fi le through a traditional file system.

## General Capabilities
- Provides redundant, scalable object storage using clusters of standardized servers capable of storing petabytes of data
- Distributed storage system for static data such as virtual machine images, photo storage, email storage, backups and archives. Having no central "brain" or master point of control provides greater scalability, redundancy and durability.
- Objects and files are written to multiple disk drives spread throughout servers in the data center, with the software responsible for ensuring data replication and integrity across the cluster.
- Storage clusters scale horizontally simply by adding new servers. Should a server or hard drive fail, the system replicates its content from other active nodes to new locations in the cluster.

## Use Cases
Object Storage has a lot of potential use cases, we won't list them all here. But here are some examples that may guide your thoughts:

- Archiving/Backup (ie. Logs, Backups, Database Dumps, etc.)
- Web Files (ie. Images, Videos, Static Content, etc.)
- Document Sharing
- Monitoring Metrics
- etc.
