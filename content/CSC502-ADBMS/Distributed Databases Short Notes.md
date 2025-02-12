| Subtopic                                                  | Mini-topic                                            |
| :-------------------------------------------------------- | :---------------------------------------------------- |
|                                                           | (Introduction and Overview)                           |
| **19.1 Homogeneous and Heterogeneous Databases**          |                                                       |
| **[[19.2 Distributed Data Storage]]**                     |                                                       |
|                                                           | - 19.2.1 Data Replication                             |
|                                                           | - 19.2.2 Data Fragmentation                           |
|                                                           |      - Horizontal Fragmentation                       |
|                                                           |      - Vertical Fragmentation                         |
|                                                           | - 19.2.3 Transparency                                 |
|                                                           |      - Fragmentation Transparency                     |
|                                                           |      - Replication Transparency                       |
|                                                           |      - Location Transparency                          |
| **[[19.3 Distributed Transactions]]**                     |                                                       |
|                                                           | - 19.3.1 System Structure                             |
|                                                           | - 19.3.2 System Failure Modes                         |
| **[[19.4 Commit Protocols]]**                             |                                                       |
|                                                           | - 19.4.1 Two-Phase Commit                             |
|                                                           | - 19.4.2 Three-Phase Commit                           |
|                                                           | - 19.4.3 Alternative Models of Transaction Processing |
|                                                           |      - Persistent Messaging                           |
|                                                           |      - Workflows                                      |
| **[[19.5 Concurrency Control in Distributed Databases]]** |                                                       |
|                                                           | 19.5.1 Locking Protocols                              |
|                                                           | - Single Lock-Manager Approach                        |
|                                                           | - Distributed Lock Manager                            |
|                                                           | - Primary Copy                                        |
|                                                           | - Majority Protocol                                   |
|                                                           | - Biased Protocol                                     |
|                                                           | - Quorum Consensus Protocol                           |
|                                                           | [[19.5.2 Timestamping]]                               |
|                                                           | 19.5.3 Replication with Weak Degrees of Consistency   |
|                                                           |      - Master-Slave Replication                       |
|                                                           |      - Multimaster Replication                        |
|                                                           | [[19.5.4 Deadlock Handling in Distributed Databases]] |
| **19.6 Availability**                                     |                                                       |
|                                                           | - 19.6.1 Majority-Based Approach                      |
|                                                           | - 19.6.2 Read One, Write All Available Approach       |
|                                                           | - 19.6.3 Site Reintegration                           |
|                                                           | - 19.6.4 Comparison with Remote Backup                |
|                                                           | - 19.6.5 Coordinator Selection                        |
|                                                           |      - Backup Coordinator                             |
|                                                           |      - Election Algorithms                            |
|                                                           |      - Bully Algorithm                                |
|                                                           | - 19.6.6 Trading Off Consistency for Availability     |
|                                                           |      - CAP Theorem                                    |
|                                                           |      - BASE Properties                                |
| **[[19.7 Distributed Query Processing]]**                 |                                                       |
|                                                           | - 19.7.1 Query Transformation                         |
|                                                           | - 19.7.2 Simple Join Processing                       |
|                                                           | - 19.7.3 Semijoin Strategy                            |
|                                                           | - 19.7.4 Join Strategies that Exploit Parallelism     |
| **19.8 Heterogeneous Distributed Databases**              |                                                       |
|                                                           | - 19.8.1 Unified View of Data                         |
|                                                           | - 19.8.2 Query Processing                             |
|                                                           |      - Wrappers                                       |
|                                                           |      - Mediator Systems                               |
|                                                           | - 19.8.3 Transaction Management in Multidatabases     |
| **19.9 Cloud-Based Databases**                            |                                                       |
|                                                           | - 19.9.1 Data Storage Systems on the Cloud            |
|                                                           |      - Data Representation                            |
|                                                           |      - JSON                                           |
|                                                           |      - Partitioning and Retrieving Data               |
|                                                           |      - Tablets                                        |
|                                                           |      - Transactions and Replication                   |
|                                                           | - 19.9.2 Traditional Databases on the Cloud           |
|                                                           | - 19.9.3 Challenges with Cloud-Based Databases        |
| **19.10 Directory Systems**                               |                                                       |
|                                                           | - 19.10.1 Directory Access Protocols                  |
|                                                           | - 19.10.2 LDAP: Lightweight Directory Access Protocol |
|                                                           |      - Data Model                                     |
|                                                           |      - Data Manipulation                              |
|                                                           |      - Distributed Directory Trees                    |

