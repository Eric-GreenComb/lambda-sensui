Worker Lambda that receives data for metaTx relay (probably same as one today)
Store calling params in db (metatx table)
Select on db which account is available to use (on accounts table) and update table with metatx_id
If non account is available finish (metatx table will have no txHash so tx will be queued)
Send tx to blockchain
Update metatx table with txHash
(s7)When mined store txReceipt on metatx table and update account table to mark account as free
If not mined in a decent time, try again with another gaslimit (or other parameters) 

Lambda to query status of a metatx

Lambda to check queued tx and start worker lambda again (triggered on s7)


tables
metatx
- id /hash
- params
- account where is being processed
- eth_txHash
- eth_transactionReceipt

accounts
- address
- blockchain
- metatx_id