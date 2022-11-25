- State Trasition Diagram
![[transactionStates.png]]

- Always do internal calculation after converting to blocks when calculating query cost. Other wise output will be incorrect due to multiplication when reading.(does not read record by record. reads block by block)