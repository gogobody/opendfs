# opendfs
单独的数据节点
事件的 active 时epoll add 时设置的，ready是epoll wait到事件准备处理时设置的

3 ：main -> process_master_cycle -> process_start_workers -> process_spawn -> worker_processer 
            -> dfs_module_worker_init -> dn_data_storage_worker_init |-> cfs_prepare_work -> cfs_faio_init -> faio_manager_init  -> faio_data_manager_init 
                                                                     |                                                          -> faio_worker_manager_init -> faio_worker_init_properties
                                                                     |                                                                                      -> faio_worker_start_thread //  开启了两个同样的线程
                                                                     |                                                          -> faio_handler_manager_init
                                                                     |                                    -> faio_register_handler // 注册 read write sendfile handler                                 
                                                                     |
                                                                     |-> blk_cache_mgmt_new_init -> blk_mem_mgmt_create -> dfs_mem_allocator_new_init -> dfs_get_commpool_allocator
                                                                     |                                                                                -> mpool_mgmt_allocator_init
                                                                     |                                                                                
                                                                     |                                                  -> blk_mblks_create -> mem_mblks_new_fn
                                                                     |                                                  -> dfs_hashtable_create -> dfs_hashtable_init
                                                                     |-> blk_report_queue_init
                                                                     
                                                                     
 

changes:
last_pos = in->buf->pos + bsize; // add bsize