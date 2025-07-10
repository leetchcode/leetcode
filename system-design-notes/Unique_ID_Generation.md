# Unique ID Generation

## Why random IDs are bad ?
- Due to poor index locality
- Non-time-ordered UUIDs values generated in succession are not sequential. 
- The randomly generated values will not be clustered to each other in a database index, and 
  thus inserts will be performed at random locations. This random insertion can negatively affect the performance on common index data structures such as B-tree and its variants.
- With non-sequential identifiers, the most recent data will be randomly dispersed within an index and lack clustering. As a result, retrieving the most recent data from a large dataset will require traversing a large number of database index pages, leading to a poor cache hit ratio (how many requests a cache is able to fill successfully, compared to how many requests it receives). 
- Compare this to the use of sequential identifiers, where the latest data is logically arranged on the right-most part of an index, allowing it to be far more cache-friendly.

## How does Instagram ID generation work ?
[Sharding & IDs at Instagram](https://instagram-engineering.com/sharding-ids-at-instagram-1cf5a71e5a5c)
### Requirements
- Generated IDs should be sortable by time (so a list of photo IDs, for example, could be sorted without fetching more information about the photos)
- IDs should ideally be 64 bits (for smaller indexes, and better storage in systems like Redis)
- The system should introduce as few new ‘moving parts’ as possible — a large part of how we’ve been able to scale Instagram with very few engineers is by choosing simple, easy-to-understand solutions that we trust.

### Solution
- Created a fixed number of logical shards
- Map logical shards to physical DB servers (in code)
- Created a custom epoch
- Created a format where first few bits were for timestamp from the custom epoch followed by shard_id and followed by sequence_id (per shard)
- All of the above logic was included as a stored procedure in DB and specified in table create schema to be used as auto id generation custom function 
  
  
