# polkadot-devcamp-project-2022
Team 3 - Project Idea
Team Members</br>
@ck </br>
@Vijendr </br>
@rishikesh </br>
@sinzii </br>
# General Idea </br>
A secured messaging application </br>
One can send messages to others using substrate address as their identity </br>
Everyone will get a copy of the message, and the message content of each copy will be encrypted using each one’s public key. So only the one with an appropriate private key can decrypt the message. </br>
The message content will be stored on-chain with limited characters or on an external decentralized service like IPFS </br>
To limit the scope of the project, we’ll try to implement one-to-one messaging mechanism, one-to-many messaging will be an improvement point for the future. </br>
# Challenges</br>
Encrypt/decrypt the message using public/private key </br>
When to encrypt the message </br>
On-chain: how is it affect block time? </br>
Off-chain:</br>
Off-chain worker: https://docs.substrate.io/v3/concepts/off-chain-features/ </br>
On Dapp: </br>
Encrypt the message on Dapp and store the message to IPFS to get content hash </br>
Then use the content hash to submit the extrinsic </br>
Where/how to store the encrypted message content </br>
On-chain</br> 
IPFS Services</br>
https://www.kaleido.io/blockchain-platform/ipfs-file-store</br>
https://www.pinata.cloud/</br>
…
Tokenomic</br>
Introduce a utility token to charge for sending messages</br>
Implementation</br>
Pallet: messaging</br>
Data Modeling</br>
MessageId = u64</br>
enum Owner (Sender, Receiver)</br>
Message</br>
id: MessageId</br>
sender: AccountId</br>
receiver: AccountId</br>
content: String</br>
Raw encrypted content</br>
IPFS hash</br>
created_at: timestamp</br>
owner: Owner - the message content will be encrypted by the owner’s public key</br>
Storage</br>
StorageValue: next_message_id: u64</br>
Since we don’t have an auto-increment id like in relational databases, this will be used as the message-id for new messages,</br>
This looks like a sequence in PostgreSQL, but we’ll need to increase the value manually.</br>
The first message-id will start from 0 and will increase one by one as new messages are created</br>
StorageMap: message_by_message_id</br>
MessageId → Message</br>
StorageDoubleMap: message_ids_by_account_ids</br>
AccountId_1, AccountId_2 → List<MessageId></br>
For each one-to-one conversation between A1 & A2, we’ll store:</br>
A1, A2 → List<MessageId>: a list of messages encrypted by A1’s public key</br>
A2, A1 → List<MessageId>: a list of messages encrypted by A2’s public key</br>
StorageMap: conversations_by_account_id</br>
AccountId → List<AccountId></br>
For an account A1 that has recent conversations with A2, A3, A4, we’ll store:</br>
A1 → [A2, A3, A4]</br>
Runtime API</br>
New message</br>
Get recent conversations for an account</br>
Get the list of messages for a conversation</br>
RPC</br>


Consensus Engine: AURA</br>
Tokenomic </br>
Dapp </br>
Connect to wallet Polkadot.js / SubWallet, select an account to send messages </br>
List all recent conversations</br>
View detail conversation</br>
Reply to a conversation</br>
Compose a new message to a new address</br>
New messages should be synced in realtime via RPC websocket</br>
Todo</br>
Detail out proposal</br>
Setup code repository for substrate blockchain & dapp</br>
Pallet & Runtime development</br>
Dapp development</br>
Launching</br>
Submit the codebase</br>
Demo & presentation</br>

# Further Improvements</br>
Allow register human-readable name for a specific address, and use that name to send messages instead of using a long address</br>
One-to-many messaging


