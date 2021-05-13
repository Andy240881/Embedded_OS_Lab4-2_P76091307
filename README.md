# Embedded_OS_Lab4-2_P76091307
## Step 1(show free block list in console)
* Implement the vPrintFreeList function in heap_2.c
* Main idea
```c=
node = &xStart;
while(node != &xEnd){
    sprintf(data, "%p %0d %0d %p\n\r",node,8,node->xBlockSize,(BaseType_t)node + (BaseType_t)node->xBlockSize);
    HAL_UART_Transmit(&huart2,(uint8_t*)data,strlen(data),0xffff);
    node = node->pxNextFreeBlock;
}
```
## Step 2(Merge free blocks in the list) 
* Modifying prvInsertBlockIntoFreeList code in heap_2.c to implement memory merge.
* Before prvInsertBlockIntoFreeList insert the new block, check the FreeBlockList for mergeable blocks.
    * condition 1:pxBlockToInsert's end address is the start address of  the block in FreeBlockList.
    * condition 2:pxBlockToInsert's start address is the end address of  the block in FreeBlockList.