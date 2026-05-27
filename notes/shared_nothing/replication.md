The problem is when the same large dataset is copied in all nodes, what if data is changed?

# 1. Fundamentals

- One **leader** node creates new data, and **followers** copy it.
- Leader has read/write, followers have read-only.
- In **synchronous** mode, only one healthy follower is synchronous, the rest are asynchronous. (*semi-synchronous*)
- **Catchup recovery**: Follower failure
- **Failover**: Leader failure
- Leader logs every write events.
- Beware of **replication lag** between followers. Sometimes latter data can comes before the previous. -> requires **Consistent prefix reads** guarantee.
- To prevent lag:
  - Read-after-write consistency
  - Monotonic reads
  - Constistent prefix read

-------------------------------------------

# 2. Algorithms

## Single-leader

- One leader
- Only one can write leader at a time.

## Multi-leader

- Each leader acts as a follower to other leaders.
- Imagine synced apps on phones when they are offline. Where phone is a leader
- Another example is collaborative editing apps like Google Docs.
- Multiple can write leaders at a time.
- Leader topologies: Circular, Star, All-to-all

## Leaderless

- Concurrence writes
- Last write wins (LWW)