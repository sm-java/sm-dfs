# SM-DFS Requirements for a distributed file System

####Introduction
Users create and manipulate files that may reside in multiple places, ranging from local machine to mobile phones. E.g. A user may create a file in his or her local desktop, upload it to a network drive for local access from multiple machines or upload it to the cloud and access it via a mobile device. Therefore, files can be viewed and manipulated from multiple devices and stored in multiple locations. There is a need to synchronize changes to these files made from multiple devices and locations. 

####Objectives
1. Seamlessly store files in a local or remote cluster for high availability.
2. Provide optimal storage of files in order to minimize storage needs
3. Provide policy based archiving of files
4. Maintain versioning accross local or remote stores.
5. Provide storage of sensitive files in a secure manner.

####Features
1. Can choose no replication or different replication level, rack and data center aware
2. Automatic master servers failover - no single point of failure (SPOF)
3. Automatic Gzip compression depending on file mime type
4. Automatic compaction to reclaimed disk spaces after deletion or update
5. Servers in the same cluster can have different disk spaces, file systems, OS etc.
6. Adding/Removing servers does not cause any data re-balancing
7. Optional filer server provides "normal" directories and files via http
8. Optionally fix the orientation for jpeg pictures
9. Support Etag, Accept-Range, Last-Modified, etc.


####Design Goals
1. SM-DFS interface should be as close to any other file system.
2. Ability to plug-in multiple file system adaptors

