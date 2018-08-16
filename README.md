# LinkedListWithReadWriteLock

对链表的读写锁, 伪代码如下:

```
class linked_list {

    node* head;
    ...
    int readCount;
    mutex readMutex;
    mutex writeMutex;

    void getReadLock() {
        readMutex.lock();

        if(readCount == 0) {
            writeMutex.lock();
        }

        readCount++;
        readMutex.release();
    }

    void releaseReadLock() {
      readMutex.lock();
      readCount--;

      if(readCount == 0) {
          writeMutex.release();
      }
      
      readMutex.release();
    }

    void getWriteLock() {
      writeMutex.lock();
    }

    void releaseWriteLock() {
      writeMutex.lock();
    }

}
```
