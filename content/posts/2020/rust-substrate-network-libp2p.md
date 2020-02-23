---
title: "Rust Substrate Network Libp2p"
date: 2020-02-23T10:15:01+08:00
draft: true
---

主要考察`trait`，因为它类似于`interface`的概念
### Substrate是什么

[Substrate](https://substrate.dev/)是一个基本开箱即用的区块链框架

### Substrate Network包含了什么

#### chain.rs

```rust
pub trait Client<Block: BlockT>: Send + Sync {
	/// Get blockchain info.
	fn info(&self) -> BlockchainInfo<Block>;

	/// Get block status.
	fn block_status(&self, id: &BlockId<Block>) -> Result<BlockStatus, Error>;

	/// Get block hash by number.
	fn block_hash(&self, block_number: NumberFor<Block>) -> Result<Option<Block::Hash>, Error>;

	/// Get block header.
	fn header(&self, id: &BlockId<Block>) -> Result<Option<Block::Header>, Error>;

	/// Get block body.
	fn body(&self, id: &BlockId<Block>) -> Result<Option<Vec<Block::Extrinsic>>, Error>;

	/// Get block justification.
	fn justification(&self, id: &BlockId<Block>) -> Result<Option<Justification>, Error>;

	/// Get block header proof.
	fn header_proof(&self, block_number: NumberFor<Block>)
		-> Result<(Block::Header, StorageProof), Error>;

	/// Get storage read execution proof.
	fn read_proof(&self, block: &Block::Hash, keys: &[Vec<u8>]) -> Result<StorageProof, Error>;

	/// Get child storage read execution proof.
	fn read_child_proof(
		&self,
		block: &Block::Hash,
		storage_key: &[u8],
		child_info: ChildInfo,
		keys: &[Vec<u8>],
	) -> Result<StorageProof, Error>;

	/// Get method execution proof.
	fn execution_proof(&self, block: &Block::Hash, method: &str, data: &[u8]) -> Result<(Vec<u8>, StorageProof), Error>;

	/// Get key changes proof.
	fn key_changes_proof(
		&self,
		first: Block::Hash,
		last: Block::Hash,
		min: Block::Hash,
		max: Block::Hash,
		storage_key: Option<&StorageKey>,
		key: &StorageKey
	) -> Result<ChangesProof<Block::Header>, Error>;

	/// Returns `true` if the given `block` is a descendent of `base`.
	fn is_descendent_of(&self, base: &Block::Hash, block: &Block::Hash) -> Result<bool, Error>;
}

pub trait FinalityProofRequestBuilder<B: BlockT>: Send {
	/// Build data blob, associated with the request.
	fn build_request_data(&mut self, hash: &B::Hash) -> Vec<u8>;
}

```

#### lib.rs

```rust
/// Extension trait for `NetworkBehaviour` that also accepts discovering nodes.
trait DiscoveryNetBehaviour {
	/// Notify the protocol that we have learned about the existence of nodes.
	///
	/// Can (or most likely will) be called multiple times with the same `PeerId`s.
	///
	/// Also note that there is no notification for expired nodes. The implementer must add a TTL
	/// system, or remove nodes that will fail to reach.
	fn add_discovered_nodes(&mut self, nodes: impl Iterator<Item = PeerId>);
}
```


#### services.rs

```rust
/// Minimum Requirements for a Hash within Networking
pub trait ExHashT: std::hash::Hash + Eq + std::fmt::Debug + Clone + Send + Sync + 'static {}

pub trait TransactionPool<H: ExHashT, B: BlockT>: Send + Sync {
	/// Get transactions from the pool that are ready to be propagated.
	fn transactions(&self) -> Vec<(H, B::Extrinsic)>;
	/// Get hash of transaction.
	fn hash_of(&self, transaction: &B::Extrinsic) -> H;
	/// Import a transaction into the pool.
	///
	/// Peer reputation is changed by reputation_change if transaction is accepted by the pool.
	fn import(
		&self,
		report_handle: ReportHandle,
		who: PeerId,
		reputation_change_good: ReputationChange,
		reputation_change_bad: ReputationChange,
		transaction: B::Extrinsic,
	);
	/// Notify the pool about transactions broadcast.
	fn on_broadcasted(&self, propagations: HashMap<H, Vec<String>>);
	/// Get transaction by hash.
	fn transaction(&self, hash: &H) -> Option<B::Extrinsic>;
}

/// Trait for providing information about the local network state
pub trait NetworkStateInfo {
	/// Returns the local external addresses.
	fn external_addresses(&self) -> Vec<Multiaddr>;

	/// Returns the local Peer ID.
	fn local_peer_id(&self) -> PeerId;
}
```
