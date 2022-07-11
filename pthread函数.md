# pthread_cond_signal 
## pthread_cond_signal does not unlock the mutex (it can't as it has no reference to the mutex, so how could it know what to unlock?) In fact, the signal need not have any connection to the mutex; the signalling thread does not need to hold the mutex, though for most algorithms based on condition variables it will.
