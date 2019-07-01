# service_apis
These APIs are implemented with a Postgresql database. The database consists of following tables.  
devices - This table has attributes did(device-id) and accessibility(public or admin). It contains list of devices.  
users - This table has attributes uid(user-id), salt, hash and type(user or admin). It contanis information about the users.  
groups - This table has attributes uid(user-id), device_list and gid(group-id). It contains list of groups made by users. 
reservations - This table has attributes rid(reservation-id), rst(reservation start-time), ret(reservation end-time), st(start-time), et(start-time), state, frequency, duration. It conatins information regarding the reservation time. 
reservations_info - This table has attributes rid(reservation-id), uid(user-id), priority and cid(channel-id). It contains reservation information. 
device_state - This table has attributes rid(reservation-id) and device_list. It contains information about devices in a reservation. 
configure - This table has attributes rid(reservation-id), configurations, type(sync or async), id. It contains the device configurations.  
write_op - This table has attributes rid(reservation-id), content, type(sync or async), id. It contains the device content. 
