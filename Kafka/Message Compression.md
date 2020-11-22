When sending text data it's important to set the compression. It is set on a [[Producers]].
There are a number of values that can be set to change the type of compression.
![[message_compresion.png]]
The larger the batch size the more important the compression is.

## Benefits
- much smaller requests.
- faster data transfer.
- better throughput.
## Disadvantages
- more cpu heavy on producers and brokers to compress and decompress.
- maybe be slower depending on the use case.