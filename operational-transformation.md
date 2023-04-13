### [Collaborative editing](https://conclave-team.github.io/conclave-site/?ref=hackernoon.com#operational-transformation-ot)
1. Each client maintains a local copy of the document
2. Client edits the local copy of the document. Client sends local changes to the server, server tracks the versions and relays the changes to the other clients.
3. Client applies changes from the remote client such that the intention is preserved and all copies converge. Most probably the changes have occurred concurrently(i.e remote client didn't see the changes of the local server before making changes on the remote client).
   1. OT
      1. Transforms the indices of the remote changes to the indices of the local change such that the intention is preserved.
      2. The above transformation, makes the insertChar, deleteChar operations commutative.
   2. CRDTs
      1. Assign a unique position to each character. Position doesn't change even after the insertion and deletion of the characters. Insert new chars in fractional positions.
      2. Apply the operations on the characters at specified positions from remote client. The operations are commutative and idempotent.
      3. See https://conclave-team.github.io/conclave-site/?ref=hackernoon.com#operational-transformation-ot for detailed explanation.

#### Theoretical treatise of the collaborative editing problem
#### Collaborative editing
1. Formalized [skeleton](https://en.wikipedia.org/wiki/Operational_transformation) of solutions that use OT algorithms
   1. Replicated document storage, where each client has their own copy of the document. 
   2. Clients operate on their local copies in a lock-free, non-blocking manner, and the changes are then propagated to the rest of the clients
   3. This model ensures the client high responsiveness in an otherwise high-latency environment such as the Internet.
   4. When a client receives the changes propagated from another client, it typically transforms the changes before executing them.
   5. Transformation transforms the positions/indices of the changes to the current local version positions/indices since they evolved from a common base.
   6. The transformation ensures that application-dependent consistency criteria (invariants) are maintained by all sites.
2. !!! Not important, fully theoretical. Consistency models for collaborative editing systems with multiple repositories.
   1. CC model
      1. Causality preservation. Happened before relationship is preserved. Ensures the execution order of causally dependent operations be the same as their natural cause-effect order during the process of collaboration
      2. Convergence. Document would converge/become identical eventually.
   2. CCI model.
      1. Causality
      2. Convergence
      3. Intention preservation: Ensures that the effect of executing an operation on any document state be the same as the intention of the operation. The intention of an operation O is defined as the execution effect which can be achieved by applying O on the document state from which O was generated.
   3. CSM model. More formal than CCI model
      1. Causality
      2. Single-operation effects: the effect of executing any operation in any execution state achieves the same effect as in its generation state 
      3. Multi-operation effects: the effects relation of any two operations is maintained after they are both executed in any states
   4. CA model.
      1. Causality: the same definition as in CC model 
      2. Admissibility: The invocation of every operation is admissible in its execution state, i.e., every invocation must not violate any effects relation (object ordering) that has been established by earlier invocations.

#### OT
1. OT was originally invented for consistency maintenance and concurrency control in collaborative editing of plain text documents. Its capabilities have been extended and its applications expanded to include group undo, locking, conflict resolution, operation notification and compression, group-awareness, HTML/XML and tree-structured document editing, collaborative office productivity tools, application-sharing, and collaborative computer-aided media design tools.
2. Achieving the non-serializable intention preservation property has been a major technical challenge.
3. OT has been found particularly suitable for achieving convergence and intention preservation in collaborative editing systems.

### CRDT
1. A conflict-free replicated data type (CRDT) is a data structure that is replicated across multiple computers in a network, with the following features:[1][2][3][4][5][6][7][8]
   1. The application can update any replica independently, concurrently and without coordinating with other replicas.
   2. An algorithm (itself part of the data type) automatically resolves any inconsistencies that might occur.
   3. Although replicas may have different state at any particular point in time, they are guaranteed to eventually converge.
2. Optimistic replication, where all concurrent updates are allowed to go through, with inconsistencies possibly created, and the results are merged or "resolved" later. In this approach, consistency between the replicas is eventually re-established via "merges" of differing replicas. While optimistic replication might not work in the general case, there is a significant and practically useful class of data structures, CRDTs, where it does work — where it is always possible to merge or resolve concurrent updates on different replicas of the data structure without conflicts. This makes CRDTs ideal for optimistic replication.
3. There are two approaches to CRDTs, both of which can provide strong eventual consistency:
   1. Operation-based CRDTs
      1. CmRDT replicas propagate state by transmitting only the update operation. Replicas receive the updates and apply them locally. The operations are commutative. However, they are not necessarily idempotent.
      2. The communications infrastructure must therefore ensure that all operations on a replica are delivered to the other replicas, without duplication, but in any order.
      3. Low bandwidth compared to the other approach.
   2. State-based CRDTs
      1. CvRDTs send their full local state to other replicas, where the states are merged by a function which must be commutative, associative, and idempotent. The merge function provides a join for any pair of replica states, so the set of all states forms a semilattice.
      2. Easy to implement since there are no network guarantees required.
4. Implementations
   1. Redis is a distributed, highly available and scalable in-memory database that uses CRDTs for implementing globally distributed databases based on and fully compatible with Redis open source.
   2. Riak is a distributed NoSQL key-value data store based on CRDTs. League of Legends uses the Riak CRDT implementation for its in-game chat system, which handles 7.5 million concurrent users and 11,000 messages per second. Bet365, stores hundreds of megabytes of data in the Riak implementation of OR-Set.
   3. Apple implements CRDTs in the Notes app for syncing offline edits between multiple devices.
   4. A sequence, list, or ordered set CRDT can be used to build a Collaborative real-time editor, as an alternative to Operational transformation (OT).