# SPMC PubSubQueue (Fixed Type)

+ For an SPMC (Single Producer Multiple Consumers) PubSubQueue, the core design idea is that each consumer thread stores its own read index. Additionally, the producer does not check whether the queue is full, ensuring that consumers do not affect the producer.

+ To avoid the need for consumer threads to also read the write index, we can store a sequence number in each MsgHeader. Consumer threads can use this sequence number to check if there are new messages to read, thereby minimizing the overhead caused by shared variables (such as cache coherence overhead).