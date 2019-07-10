# service_apis
Documentation: https://docs.google.com/document/d/1BCaWlkWpkUXMLD1ygu3fm5EfUNDotk9zpbF8Nd0T5ZQ/edit#heading=h.cr41vnrke1qb

The APIs are used by users to sign up, create groups of devices and reserve those groups. After obtaining a reservation-id the user can configure the devices and write content to the devices. These APIs are a reference implementation of the write APIs. 
These APIs are implemented in flask with a Postgresql database. The database consists of following tables.  
devices - It contains list of devices.  
users - It contanis information about the users.  
groups - It contains list of groups made by users. 
reservations - It conatins information regarding the reservation time. 
reservations_info - It contains reservation information. 
device_state - It contains information about devices in a reservation. 
configure - It contains the device configurations.  
write_op - It contains the device content. 
