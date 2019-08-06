import requests
from flask import Flask, request, Response, jsonify, make_response
import urllib3
import logging
import json
import urllib3
import random
import psycopg2
from werkzeug.security import generate_password_hash, check_password_hash
import string
import time
import radar
from datetime import datetime,timedelta,date

from requests.adapters import HTTPAdapter

base_url = 'https://127.0.0.1'
s = requests.Session()
s.mount('https://127.0.0.1/', HTTPAdapter(pool_connections=10))
connection = psycopg2.connect(user = "myuser",password = "password",host = "127.0.0.1",port = "5432", database = "postgres")
cur = connection.cursor()

urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

logger = logging.getLogger(__name__)
logging.getLogger('urllib3').setLevel(logging.WARNING)


def signup_request(data):
	url = base_url +'/signup'
	headers = {'content-type':'application/json'}
	r = s.post(url=url, headers=headers, data=json.dumps(data), verify=False)
	return r

def create_group_request(ID,apikey,data):
	url = base_url +'/groups'
	headers = {'id': ID,'apikey': apikey,'content-type':'application/json'}
	r = s.post(url=url, headers=headers, data=json.dumps(data), verify=False)
	return r

def update_group_request(ID,apikey,data,gid):
	url = base_url +'/groups/'+gid
	headers = {'id': ID,'apikey': apikey,'content-type':'application/json'}
	r = s.put(url=url, headers=headers, data=json.dumps(data), verify=False)
	return r

def delete_group_request(ID,apikey,gid):
	url = base_url +'/groups/'+gid
	headers = {'id': ID,'apikey': apikey,'content-type':'application/json'}
	r = s.delete(url=url, headers=headers, verify=False)
	return r

def create_reservation_request(ID,apikey,data):
	url = base_url +'/reservations'
	headers = {'id': ID,'apikey': apikey,'content-type':'application/json'}
	r = s.post(url=url, headers=headers, data=json.dumps(data), verify=False)
	return r

def update_reservation_request(ID,apikey,data,rid):
	url = base_url + '/reservations/'+ rid
	headers = {'id': ID,'apikey': apikey,'content-type':'application/json'}
	r = s.put(url=url, headers=headers, data=json.dumps(data), verify=False)
	return r

def delete_reservation_request(ID,apikey,rid):
	url = base_url +'/reservations/' + rid
	headers = {'id': ID,'apikey': apikey,'content-type':'application/json'}
	r = s.delete(url=url, headers=headers, verify=False)
	return r

def create_asyncconfiguration_request(ID,apikey,data):
	url = base_url +'/async-configurations'
	headers = {'id': ID,'apikey': apikey,'content-type':'application/json'}
	r = s.post(url=url, headers=headers, data=json.dumps(data), verify=False)
	return r

def create_asyncwrite_request(ID,apikey,data):
	url = base_url +'/async-write'
	headers = {'id': ID,'apikey': apikey,'content-type':'application/json'}
	r = s.post(url=url, headers=headers, data=json.dumps(data), verify=False)
	return r

def device_status_request(ID,apikey,data):
	url = base_url + '/device-status'
	headers = {'id': ID,'apikey': apikey,'content-type':'application/json'}
	r = s.post(url=url, headers=headers, data=json.dumps(data), verify=False)
	return r

def operational_status_request(ID,apikey,data):
	url = base_url +'/operational-status'
	headers = {'id': ID,'apikey': apikey,'content-type':'application/json'}
	r = s.post(url=url, headers=headers, data=json.dumps(data),verify=False)
	return r

def create_syncconfiguration_request(ID,apikey,data):
	url = base_url +'/sync-configurations'
	headers = {'id': ID,'apikey': apikey,'content-type':'application/json'}
	r = s.post(url=url, headers=headers, data=json.dumps(data), verify=False)
	return r

def update_syncconfiguration_request(ID,apikey,data):
	url = base_url +'/sync-configurations'
	headers = {'id': ID,'apikey': apikey,'content-type':'application/json'}
	r = s.put(url=url, headers=headers, data=json.dumps(data), verify=False)
	return r

def delete_syncconfiguration_request(ID,apikey,data):
	url = base_url +'/sync-configurations'
	headers = {'id': ID,'apikey': apikey,'content-type':'application/json'}
	r = s.delete(url=url, headers=headers, data=json.dumps(data), verify=False)
	return r

def create_syncwrite_request(ID,apikey,data):
	url = base_url +'/sync-write'
	headers = {'id': ID,'apikey': apikey,'content-type':'application/json'}
	r = s.post(url=url, headers=headers, data=json.dumps(data), verify=False)
	return r

def update_syncwrite_request(ID,apikey,data):
	url = base_url +'/sync-write'
	headers = {'id': ID,'apikey': apikey,'content-type':'application/json'}
	r = s.put(url=url, headers=headers, data=json.dumps(data), verify=False)
	return r

def delete_syncwrite_request(ID,apikey,data):
	url = base_url +'/sync-write'
	headers = {'id': ID,'apikey': apikey,'content-type':'application/json'}
	r = s.delete(url=url, headers=headers, data=json.dumps(data), verify=False)
	return r

def open_channel_request(ID,apikey,data):
	url = base_url +'/open/channel'
	headers = {'id': ID,'apikey': apikey,'content-type':'application/json'}
	r = s.post(url=url, headers=headers, data=json.dumps(data), verify=False)
	return r

def suspend_channel_request(ID,apikey,data):
	url = base_url +'/suspend/channel'
	headers = {'id': ID,'apikey': apikey,'content-type':'application/json'}
	r = s.post(url=url, headers=headers, data=json.dumps(data), verify=False)
	return r

def resume_channel_request(ID,apikey,data):
	url = base_url +'/resume/channel'
	headers = {'id': ID,'apikey': apikey,'content-type':'application/json'}
	r = s.post(url=url, headers=headers, data=json.dumps(data), verify=False)
	return r

def close_channel_request(ID,apikey,data):
	url = base_url +'/close/channel'
	headers = {'id': ID,'apikey': apikey,'content-type':'application/json'}
	r = s.post(url=url, headers=headers, data=json.dumps(data), verify=False)
	return r



def signup_validcase():
	ID = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	data = {"id" :ID}
	req = signup_request(data)
	check(req,201)
	sql_delete_query = """Delete from users where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()

def signup_no_id():
	data = {}
	req = signup_request(data)
	check(req,400)

def signup_id_already_existing():
	query = """select * from users"""
    	cur.execute(query)
    	record = cur.fetchone()
	data = {"id" : record[0]}
	req = signup_request(data)
	check(req,409)

def signup_id_length_exceeded():
	data = {"id" : "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(51)])}
	req = signup_request(data)
	check(req,400)

def signup_id_not_alphanumeric():
	data = {"id" : "@".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])}
	req = signup_request(data)
	check(req,400)



def creategroup_validcase(ID, apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()	
	gn = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	data = {"group-name":gn, "resources" : [device]}
	req = create_group_request(ID,apikey,data)
	check(req,201)
	gid = ID+"-"+gn
	sql_delete_query = """Delete from groups where gid = %s"""
        cur.execute(sql_delete_query, (gid, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()


def creategroup_groupname_already_existing(ID, apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()	 
	query = """select * from groups where uid = %s"""
    	cur.execute(query, (ID, ))
    	record = cur.fetchone()
	group = record[2]
	uid,gn = group.split('-')
	data = {"group-name":gn, "resources" : [device]}
	req = create_group_request(ID,apikey,data)
	check(req,409)
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def creategroup_no_groupname(ID, apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()	 
	data = {"resources" : [device]}
	req = create_group_request(ID,apikey,data)
	check(req,201)
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def creategroup_no_body(ID, apikey):
	data = {}
	req = create_group_request(ID,apikey,data)
	check(req,400)

def creategroup_no_resources(ID, apikey):
	data = {"group-name":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])}
	req = create_group_request(ID,apikey,data)
	check(req,400)

def creategroup_admin_resources(ID, apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'admin'))
	connection.commit()	
	data = {"group-name":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)]),"resources" : [device]}
	req = create_group_request(ID,apikey,data)
	check(req,400)
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def creategroup_invalid_resources(ID, apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])	
	data = {"group-name":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)]),"resources" : [device]}
	req = create_group_request(ID,apikey,data)
	check(req,400)

def create_group_groupname_not_alphanumeric(ID, apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'admin'))
	connection.commit()	
	data = {"group-name":"@".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)]), "resources" : [device]}
	req = create_group_request(ID,apikey,data)
	check(req,400)
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def create_group_groupname_length_exceeded(ID, apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'admin'))
	connection.commit()	
	data = {"group-name": "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(51)]), "resources" : [device]}
	req = create_group_request(ID,apikey,data)
	check(req,400)
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()



def update_group_validcase(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()	
	query = """select * from groups where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	data = {"resources" : [device]}
	gid = record[2]
	req = update_group_request(ID,apikey,data,gid)
	check(req,200)
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def update_group_no_resources(ID,apikey):
	data = {}
	query = """select * from groups where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	gid = record[2]
	req = update_group_request(ID,apikey,data,gid)
	check(req,400)

def update_group_admin_resources(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'admin'))
	connection.commit()
	data = {"resources" : [device]}
	query = """select * from groups where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	gid = record[2]
	req = update_group_request(ID,apikey,data,gid)
	check(req,400)

def update_group_invalid_resources(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	data = {"resources" : [device]}
	query = """select * from groups where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	gid = record[2]
	req = update_group_request(ID,apikey,data,gid)
	check(req,400)

def update_group_gid_empty(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	data = {"resources" : [device]}
	gid = ''
	req = update_group_request(ID,apikey,data,gid)
	check(req,404)

def update_group_someoneelse_gid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	data = {"resources" : [device]}
	query = """select * from groups where uid != %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	gid = record[2]
	req = update_group_request(ID,apikey,data,gid)
	check(req,400)



def delete_group_validcase(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()	
	gn = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	data = {"group-name":gn, "resources" : [device]}
	req = create_group_request(ID,apikey,data)
	gid = ID+"-"+gn
	req = delete_group_request(ID,apikey,gid)
	check(req,200)

def delete_group_invalid_gid(ID,apikey):
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	req = delete_group_request(ID,apikey,gid)
	check(req,400)

def delete_group_gid_empty(ID,apikey):
	gid = ''
	req = delete_group_request(ID,apikey,gid)
	check(req,404)

def delete_group_someoneelse_gid(ID,apikey):
	query = """select * from groups where uid != %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	gid = record[2]
	req = delete_group_request(ID,apikey,gid)
	check(req,400)



def daterange(d1, d2):
	for n in range(int ((d2-d1).days)+1):
		yield d1+timedelta(n)



def create_reservation_validcase(ID,apikey):
	query = """select * from groups where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	gid = record[2]
	start_date = date(2020, 7, 2)
	end_date = date(2020, 12, 31)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%m-%d")
	start_time = pt + " 12:00:00"
	end_time = pt + " 14:00:00"
	data = {"gid":gid,"start-time":start_time,"end-time":end_time}
	req = create_reservation_request(ID,apikey,data)
	check(req,201)

def create_reservation_frequency_duration_given(ID,apikey):
	query = """select * from groups where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	gid = record[2]
	start_date = date(2020, 7, 2)
	end_date = date(2020, 12, 31)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%m-%d")
	start_time = pt + " 15:00:00"
	end_time = pt + " 16:00:00"
	data = {"gid":gid,"start-time":start_time,"end-time":end_time,"frequency":"hourly","duration":"1:10"}
	req = create_reservation_request(ID,apikey,data)
	check(req,201)

def create_reservation_duration_exceeds_reservationtime(ID,apikey):
	query = """select * from groups where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	gid = record[2]
	start_date = date(2020, 7, 2)
	end_date = date(2020, 12, 31)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%m-%d")
	start_time = pt + " 10:00:00"
	end_time = pt + " 12:00:00"
	data = {"gid":gid,"start-time":start_time,"end-time":end_time,"frequency":"hourly","duration":"02:02:10"}
	req = create_reservation_request(ID,apikey,data)
	check(req,400)

def create_reservation_wrong_datetime_format(ID,apikey):
	query = """select * from groups where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	gid = record[2]
	start_date = date(2020, 7, 2)
	end_date = date(2020, 12, 31)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%d-%m")
	start_time = pt + " 08:00:00"
	end_time = pt + " 10:00:00"
	data = {"gid":gid,"start-time":start_time,"end-time":end_time,"frequency":"hourly","duration":"02:02:10"}
	req = create_reservation_request(ID,apikey,data)
	check(req,400)

def create_reservation_someoneelse_gid(ID,apikey):
	query = """select * from groups where uid != %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	gid = record[2]
	start_date = date(2020, 7, 2)
	end_date = date(2020, 12, 31)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%m-%d")
	start_time = pt + " 05:00:00"
	end_time = pt + " 06:00:00"
	data = {"gid":gid,"start-time":start_time,"end-time":end_time}
	req = create_reservation_request(ID,apikey,data)
	check(req,400)

def create_reservation_no_gid(ID,apikey):
	start_date = date(2020, 7, 2)
	end_date = date(2020, 12, 31)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%m-%d")
	start_time = pt + " 02:00:00"
	end_time = pt + " 03:00:00"
	data = {"start-time":start_time,"end-time":end_time}
	req = create_reservation_request(ID,apikey,data)
	check(req,400)

def create_reservation_alreadyreserved(ID,apikey):
	query = """select * from groups where uid = %s"""		    
	cur.execute(query, (ID, ))
    	records = cur.fetchone()
	gid = records[2]
	start_date = date(2020, 7, 2)
	end_date = date(2020, 12, 31)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%m-%d")
	start_time = pt + " 06:00:00"
	end_time = pt + " 07:00:00"
	data = {"gid":gid,"start-time":start_time,"end-time":end_time}
	req = create_reservation_request(ID,apikey,data)
	data = {"gid":gid,"start-time":start_time,"end-time":end_time}
	req = create_reservation_request(ID,apikey,data)
	check(req,409)

def create_reservation_frequencygiven_noduration(ID,apikey):
	query = """select * from groups where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	gid = record[2]
	start_date = date(2020, 7, 2)
	end_date = date(2020, 12, 31)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%m-%d")
	start_time = pt + " 10:00:00"
	end_time = pt + " 12:00:00"
	data = {"gid":gid,"start-time":start_time,"end-time":end_time,"frequency":"hourly"}
	req = create_reservation_request(ID,apikey,data)
	check(req,400)

def create_reservation_invalid_frequency(ID,apikey):
	query = """select * from groups where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	gid = record[2]
	start_date = date(2020, 7, 2)
	end_date = date(2020, 12, 31)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%m-%d")
	start_time = pt + " 10:00:00"
	end_time = pt + " 12:00:00"
	data = {"gid":gid,"start-time":start_time,"end-time":end_time,"frequency":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])}
	req = create_reservation_request(ID,apikey,data)
	check(req,400)

def create_reservation_endtime_before_starttime(ID,apikey):
	query = """select * from groups where uid != %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	gid = record[2]
	start_date = date(2020, 7, 2)
	end_date = date(2020, 12, 31)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%m-%d")
	start_time = pt + " 14:00:00"
	end_time = pt + " 12:00:00"
	data = {"gid":gid,"start-time":start_time,"end-time":end_time}
	req = create_reservation_request(ID,apikey,data)
	check(req,400)

def create_reservation_starttime_already_passed(ID,apikey):
	query = """select * from groups where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	gid = record[2]
	start_date = date(2018, 7, 2)
	end_date = date(2018, 12, 31)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%m-%d")
	start_time = pt + " 10:00:00"
	end_time = pt + " 12:00:00"
	data = {"gid":gid,"start-time":start_time,"end-time":end_time}
	req = create_reservation_request(ID,apikey,data)
	check(req,400)

def create_reservation_no_starttime_noendtime(ID,apikey):
	query = """select * from groups where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	gid = record[2]
	data = {"gid":gid}
	req = create_reservation_request(ID,apikey,data)
	check(req,400)

def create_reservation_no_starttime(ID,apikey):
	query = """select * from groups where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	gid = record[2]
	start_date = date(2020, 7, 2)
	end_date = date(2020, 12, 31)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%m-%d")
	end_time = pt + " 12:00:00"
	data = {"gid":gid,"end-time":end_time}
	req = create_reservation_request(ID,apikey,data)
	check(req,400)

def create_reservation_no_endtime(ID,apikey):
	query = """select * from groups where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	gid = record[2]
	start_date = date(2020, 7, 2)
	end_date = date(2020, 12, 31)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%m-%d")
	start_time = pt + " 10:00:00"
	data = {"gid":gid,"frequency":"hourly","start-time":start_time}
	req = create_reservation_request(ID,apikey,data)
	check(req,400)



def update_reservation_wrong_datetime_format(ID,apikey):
	query = """select * from reservations_info where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	start_date = date(2020, 7, 2)
	end_date = date(2020, 12, 31)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%d-%m")
	start_time = pt + " 10:00:00"
	end_time = pt + " 12:00:00"
	data = {"start-time":start_time,"end-time":end_time}
	req = update_reservation_request(ID,apikey,data,rid)
	check(req,400)

def update_reservation_invalid_frequency(ID,apikey):
	query = """select * from reservations_info where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	data = {"frequency":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])}
	req = update_reservation_request(ID,apikey,data,rid)
	check(req,400)

def update_reservation_no_starttime_noendtime(ID,apikey):
	query = """select * from groups where uid = %s"""		    
	cur.execute(query, (ID, ))
    	records = cur.fetchone()
	gid = records[2]
	start_date = date(2020, 7, 2)
	end_date = date(2020, 12, 31)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%m-%d")
	start_time = pt + " 06:00:00"
	end_time = pt + " 07:00:00"
	query = """select * from reservations_info where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	data = {"gid":gid,"start-time":start_time,"end-time":end_time}
	req = create_reservation_request(ID,apikey,data)
	data = {"duration":"1:08"}
	req = update_reservation_request(ID,apikey,data,rid)
	check(req,200)

def update_reservation_invalid_rid(ID,apikey):
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	start_date = date(2020, 2, 2)
	end_date = date(2020, 6, 30)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%m-%d")
	start_time = pt + " 10:00:00"
	end_time = pt + " 12:00:00"
	data = {"start-time":start_time,"end-time":end_time}
	req = update_reservation_request(ID,apikey,data,rid)
	check(req,400)

def update_reservation_someoneelse_rid(ID,apikey):
	query = """select * from reservations_info where uid != %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	start_date = date(2020, 7, 2)
	end_date = date(2020, 12, 31)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%m-%d")
	start_time = pt + " 10:00:00"
	end_time = pt + " 12:00:00"
	data = {"start-time":start_time,"end-time":end_time}
	req = update_reservation_request(ID,apikey,data,rid)
	check(req,400)

def update_reservation_alreadyreserved(ID,apikey):
	start_date = date(2020, 7, 2)
	end_date = date(2020, 12, 31)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%m-%d")
	start_time = pt + " 10:00:00"
	end_time = pt + " 12:00:00"
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	stime = datetime.strptime(start_time, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	etime = datetime.strptime(end_time, '%Y-%m-%d %H:%M:%S')
	est = time.mktime(etime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority) VALUES(%s,%s,%s)""",(rid,ID,3))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	rid2 = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid2,est+160,est+220,est+160,est+220,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority) VALUES(%s,%s,%s)""",(rid2,ID,3))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid2,json.dumps([device])))
	connection.commit()
	data = {"start-time":start_time,"end-time":end_time}
	req = update_reservation_request(ID,apikey,data,rid2)
	check(req,409)

def update_reservation_invalid_frequency(ID,apikey):
	query = """select * from reservations_info where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	start_date = date(2020, 7, 2)
	end_date = date(2020, 12, 31)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%m-%d")
	start_time = pt + " 10:00:00"
	end_time = pt + " 12:00:00"
	data = {"start-time":start_time,"end-time":end_time,"frequency":"ant"}
	req = update_reservation_request(ID,apikey,data,rid)
	check(req,400)

def update_reservation_endtime_before_starttime(ID,apikey):
	query = """select * from reservations_info where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	start_date = date(2020, 7, 2)
	end_date = date(2020, 12, 31)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%m-%d")
	start_time = pt + " 14:00:00"
	end_time = pt + " 12:00:00"
	data = {"start-time":start_time,"end-time":end_time}
	req = update_reservation_request(ID,apikey,data,rid)
	check(req,400)

def update_reservation_starttime_already_passed(ID,apikey):
	query = """select * from reservations_info where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	start_date = date(2018, 7, 2)
	end_date = date(2018, 12, 31)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%m-%d")
	start_time = pt + " 10:00:00"
	end_time = pt + " 12:00:00"
	data = {"start-time":start_time,"end-time":end_time}
	req = update_reservation_request(ID,apikey,data,rid)
	check(req,400)

def update_reservation_duration_exceeds_reservationtime(ID,apikey):
	query = """select * from reservations_info where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	start_date = date(2020, 7, 2)
	end_date = date(2020, 12, 31)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%m-%d")
	start_time = pt + " 10:00:00"
	end_time = pt + " 12:00:00"
	data = {"start-time":start_time,"end-time":end_time,"duration":"2:10:00"}
	req = update_reservation_request(ID,apikey,data,rid)
	check(req,400)

def update_reservation_no_rid(ID,apikey):
	rid = ''
	start_date = date(2020, 7, 2)
	end_date = date(2020, 12, 31)
	for dt in daterange(start_date, end_date):
		pt = dt.strftime("%Y-%m-%d")
	start_time = pt + " 10:00:00"
	end_time = pt + " 12:00:00"
	data = {"start-time":start_time,"end-time":end_time,"duration":"2:10:00"}
	req = update_reservation_request(ID,apikey,data,rid)
	check(req,404)



def delete_reservation_no_rid(ID,apikey):
	rid = ''
	req = delete_reservation_request(ID,apikey,rid)
	check(req,404)

def delete_reservation_someoneelse_rid(ID,apikey):
	query = """select * from reservations_info where uid != %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	req = delete_reservation_request(ID,apikey,rid)
	check(req,400)

def delete_reservation_invalid_rid(ID,apikey):
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	req = delete_reservation_request(ID,apikey,rid)
	check(req,400)

def delete_reservation_valid_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority) VALUES(%s,%s,%s)""",(rid,ID,3))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	req = delete_reservation_request(ID,apikey,rid)
	check(req,200)



def open_channel_validcase(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority) VALUES(%s,%s,%s)""",(rid,ID,3))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	body = {"rid" :rid}
	req = open_channel_request(ID,apikey,body)
	check(req,200)

def open_channel_no_rid(ID,apikey):
	body = {"rid": ""}
	req = open_channel_request(ID,apikey,body)
	check(req,400)

def open_channel_someoneelse_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(25)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	uid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	salt = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	apikey = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(32)])
	has = generate_password_hash(uid + salt + apikey)
	cur.execute("""INSERT INTO users (uid,salt,hash,type) VALUES(%s,%s,%s,%s)""",(uid,salt,has,"user"))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	gid = uid+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,uid,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority) VALUES(%s,%s,%s)""",(rid,uid,3))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	body = {"rid": rid}
	req = open_channel_request(ID,apikey,body)
	check(req,401)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (uid, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()
	sql_query = """Delete from users where uid = %s"""
        cur.execute(sql_query, (uid, ))
        connection.commit()

def open_channel_invalid_rid(ID,apikey):
	body = {"rid": "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])}
	req = open_channel_request(ID,apikey,body)
	check(req,400)

def open_channel_outside_reservationtime(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst+60,rst+120,rst+60,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority) VALUES(%s,%s,%s)""",(rid,ID,3))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	body = {"rid": rid}
	req = open_channel_request(ID,apikey,body)
	check(req,405)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def open_channel_when_high_priority_task_running(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,1,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	rid1 = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid1,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority) VALUES(%s,%s,%s)""",(rid1,ID,3))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid1,json.dumps([device])))
	connection.commit()
        now_seconds = time.mktime(currentDT.timetuple())
	body = {"rid" :rid1}
	req = open_channel_request(ID,apikey,body)
	check(req,409)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid1, ))
        connection.commit()
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid1, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid1, ))
        connection.commit()
	


def suspend_channel_someoneelse_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(25)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	uid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	salt = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	apikey = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(32)])
	has = generate_password_hash(uid + salt + apikey)
	cur.execute("""INSERT INTO users (uid,salt,hash,type) VALUES(%s,%s,%s,%s)""",(uid,salt,has,"user"))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	gid = uid+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,uid,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority) VALUES(%s,%s,%s)""",(rid,uid,3))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	body = {"rid": rid}
	req = suspend_channel_request(ID,apikey,body)
	check(req,401)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (uid, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()
	sql_query = """Delete from users where uid = %s"""
        cur.execute(sql_query, (uid, ))
        connection.commit()

def suspend_channel_valid_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	body = {"rid": rid}
	req = suspend_channel_request(ID,apikey,body)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def suspend_channel_invalid_rid(ID,apikey):
	body = {"rid" : "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])}
	req = suspend_channel_request(ID,apikey,body)
	check(req,400)

def suspend_channel_without_opening(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority) VALUES(%s,%s,%s)""",(rid,ID,3))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	body = {"rid": rid}
	req = suspend_channel_request(ID,apikey,body)
	check(req,400)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def suspend_channel_valid_rid_invalid_cid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	body = {"rid" :rid,"cid" :"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])}
	req = suspend_channel_request(ID,apikey,body)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def suspend_channel_valid_cid_invalid_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	body = {"cid" :cid,"rid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])}
	req = suspend_channel_request(ID,apikey,body)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def suspend_channel_valid_cid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	body = {"cid": cid}
	req = suspend_channel_request(ID,apikey,body)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def suspend_channel_no_ridandcid(ID,apikey):
	body = {}
	req = suspend_channel_request(ID,apikey,body)
	check(req,400)



def resume_channel_someoneelse_rid(ID,apikey):
	query = """select * from reservations_info where uid != %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	body = {"rid": rid}
	req = resume_channel_request(ID,apikey,body)
	check(req,400)

def resume_channel_valid_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"paused","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	body = {"rid" :rid}
	req = resume_channel_request(ID,apikey,body)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def resume_channel_invalid_rid(ID,apikey):
	body = {"rid" :"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])}
	req = resume_channel_request(ID,apikey,body)
	check(req,400)

def resume_channel_without_opening(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority) VALUES(%s,%s,%s)""",(rid,ID,3))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	body = {"rid" :rid}
	req = resume_channel_request(ID,apikey,body)
	check(req,400)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def resume_channel_without_suspending(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	body = {"rid" :rid}
	req = resume_channel_request(ID,apikey,body)
	check(req,400)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def resume_channel_valid_rid_invalid_cid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"paused","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	body = {"rid" :rid ,"cid" :"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])}
	req = resume_channel_request(ID,apikey,body)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def resume_channel_valid_cid_invalid_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"paused","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	body = {"cid" :cid ,"rid" :"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])}
	req = resume_channel_request(ID,apikey,body)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def resume_channel_valid_cid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"paused","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	body = {"cid" :cid}
	req = resume_channel_request(ID,apikey,body)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def resume_channel_no_ridandcid(ID,apikey):
	body = {}
	req = resume_channel_request(ID,apikey,body)
	check(req,400)



def close_channel_someoneelse_rid(ID,apikey):
	query = """select * from reservations_info where uid != %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	body = {"rid": rid}
	req = close_channel_request(ID,apikey,body)
	check(req,400)

def close_channel_valid_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	body = {"rid" :rid}
	req = close_channel_request(ID,apikey,body)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def close_channel_invalid_rid(ID,apikey):
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	body = {"rid" :rid}
	req = close_channel_request(ID,apikey,body)
	check(req,400)

def close_channel_without_opening(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"inactive","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority) VALUES(%s,%s,%s)""",(rid,ID,3))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	body = {"rid" :rid}
	req = close_channel_request(ID,apikey,body)
	check(req,400)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def close_channel_valid_rid_invalid_cid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	body = {"rid" :rid,"cid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])}
	req = close_channel_request(ID,apikey,body)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def close_channel_valid_cid_invalid_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	body = {"cid" :cid,"rid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])}
	req = close_channel_request(ID,apikey,body)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def close_channel_valid_cid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	body = {"cid" :cid}
	req = close_channel_request(ID,apikey,body)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def close_channel_no_ridandcid(ID,apikey):
	body = {}
	req = close_channel_request(ID,apikey,body)
	check(req,400)



def create_syncconfiguration_validcase(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid" : rid, "configurations": {"volume":80}}
	req = create_syncconfiguration_request(ID,apikey,data)
	check(req,200)	
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_query = """Delete from configure where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()
	
def create_syncconfiguration_already_configured(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"volume":80})
	cur.execute("""INSERT INTO configure (rid,configurations,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid" : rid, "configurations": {"volume":80}}
	req = create_syncconfiguration_request(ID,apikey,data)
	check(req,405)	
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_query = """Delete from configure where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def create_syncconfiguration_valid_did(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid" : rid, "configurations": {"volume":80},"id":[device]}
	req = create_syncconfiguration_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_query = """Delete from configure where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def create_syncconfiguration_no_configurations(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid" : rid}
	req = create_syncconfiguration_request(ID,apikey,data)
	check(req,400)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def create_syncconfiguration_invalid_did(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid" : rid, "configurations": {"volume":80},"id":["".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])]}
	req = create_syncconfiguration_request(ID,apikey,data)
	check(req,400)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def create_syncconfiguration_unreserved_did(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	d2 = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(d2,'public'))
	connection.commit()
	data = {"rid" : rid,"id":[d2],"configurations": {"volume":80}}
	req = create_syncconfiguration_request(ID,apikey,data)
	check(req,400)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def create_syncconfiguration_no_ridandcid(ID,apikey):
	data = {"configurations": {"volume":80}}
	req = create_syncconfiguration_request(ID,apikey,data)
	check(req,400)

def create_syncconfiguration_someoneelse_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(25)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	uid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	apikey = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(32)])
	salt = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	has = generate_password_hash(uid + salt + apikey)
	cur.execute("""INSERT INTO users (uid,salt,hash,type) VALUES(%s,%s,%s,%s)""",(uid,salt,has,"user"))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	gid = uid+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,uid,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,uid,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid":rid,"configurations": {"volume":80}}
	req = create_syncconfiguration_request(ID,apikey,data)
	check(req,401)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (uid, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()
	sql_query = """Delete from users where uid = %s"""
        cur.execute(sql_query, (uid, ))
        connection.commit()

def create_syncconfiguration_no_cid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid":rid,"configurations": {"volume":80},"id":[device]}
	req = create_syncconfiguration_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_query = """Delete from configure where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def create_syncconfiguration_no_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"cid":cid,"configurations": {"volume":80},"id":[device]}
	req = create_syncconfiguration_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_query = """Delete from configure where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def create_syncconfiguration_invalid_cidandrid(ID,apikey):
	data = {"rid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)]),"cid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)]),"configurations": {"volume":80}}
	req = create_syncconfiguration_request(ID,apikey,data)
	check(req,400)

def create_syncconfiguration_valid_rid_invalid_cid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid":rid,"cid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)]),"configurations": {"volume":80},"id":[device]}
	req = create_syncconfiguration_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_query = """Delete from configure where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def create_syncconfiguration_valid_cid_invalid_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)]),"cid":cid,"configurations": {"volume":80},"id":[device]}
	req = create_syncconfiguration_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_query = """Delete from configure where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def create_syncconfiguration_not_operation_time(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst+60,rst+120,rst+60,rst+120,"inactive","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority) VALUES(%s,%s,%s)""",(rid,ID,3))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid":rid,"configurations": {"volume":80},"id":[device]}
	req = create_syncconfiguration_request(ID,apikey,data)
	check(req,400)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()



def update_syncconfiguration_no_configurations_made(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid" : rid}
	req = update_syncconfiguration_request(ID,apikey,data)
	check(req,404)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def update_syncconfiguration_someoneelse_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(25)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	uid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	apikey = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(32)])
	salt = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	has = generate_password_hash(uid + salt + apikey)
	cur.execute("""INSERT INTO users (uid,salt,hash,type) VALUES(%s,%s,%s,%s)""",(uid,salt,has,"user"))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	gid = uid+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,uid,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,uid,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"volume":80})
	cur.execute("""INSERT INTO configure (rid,configurations,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid": rid ,"configurations": {"volume":80}}
	req = update_syncconfiguration_request(ID,apikey,data)
	check(req,401)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_query = """Delete from configure where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (uid, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()
	sql_delete_query = """Delete from users where uid = %s"""
        cur.execute(sql_delete_query, (uid, ))
        connection.commit()

def update_syncconfiguration_no_ridandcid(ID,apikey):
	data = {"configurations": {"volume":80}}
	req = update_syncconfiguration_request(ID,apikey,data)
	check(req,400)

def update_syncconfiguration_no_cid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"volume":80})
	cur.execute("""INSERT INTO configure (rid,configurations,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid":rid,"configurations": {"volume":80}}
	req = update_syncconfiguration_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_query = """Delete from configure where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def update_syncconfiguration_no_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"volume":80})
	cur.execute("""INSERT INTO configure (rid,configurations,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"cid":cid,"configurations": {"volume":80}}
	req = update_syncconfiguration_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_query = """Delete from configure where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def update_syncconfiguration_validcase(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"volume":80})
	cur.execute("""INSERT INTO configure (rid,configurations,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid" : rid, "configurations": {"volume":80}}
	req = update_syncconfiguration_request(ID,apikey,data)
	check(req,200)	
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_query = """Delete from configure where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def update_syncconfiguration_no_configurations(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"volume":80})
	cur.execute("""INSERT INTO configure (rid,configurations,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid" : rid}
	req = update_syncconfiguration_request(ID,apikey,data)
	check(req,400)	
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_query = """Delete from configure where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def update_syncconfiguration_valid_cid_invalid_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"volume":80})
	cur.execute("""INSERT INTO configure (rid,configurations,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)]),"cid":cid,"configurations": {"volume":80}}
	req = update_syncconfiguration_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_query = """Delete from configure where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()
	
def update_syncconfiguration_valid_rid_invalid_cid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"volume":80})
	cur.execute("""INSERT INTO configure (rid,configurations,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"cid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)]),"rid":rid,"configurations": {"volume":80}}
	req = update_syncconfiguration_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_query = """Delete from configure where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def update_syncconfiguration_invalid_cidandrid(ID,apikey):
	data = {"rid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)]),"cid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)]),"configurations": {"volume":80}}
	req = update_syncconfiguration_request(ID,apikey,data)
	check(req,400)

def update_syncconfiguration_not_operation_time(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"inactive","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority) VALUES(%s,%s,%s)""",(rid,ID,3))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"volume":80})
	cur.execute("""INSERT INTO configure (rid,configurations,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid":rid,"configurations": {"volume":80}}
	req = update_syncconfiguration_request(ID,apikey,data)
	check(req,400)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_query = """Delete from configure where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()



def delete_syncconfiguration_no_configurations_made(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid" : rid}
	req = delete_syncconfiguration_request(ID,apikey,data)
	check(req,404)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()


def delete_syncconfiguration_someoneelse_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(25)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	uid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	apikey = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(32)])
	salt = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	has = generate_password_hash(uid + salt + apikey)
	cur.execute("""INSERT INTO users (uid,salt,hash,type) VALUES(%s,%s,%s,%s)""",(uid,salt,has,"user"))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,uid,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,uid,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"volume":80})
	cur.execute("""INSERT INTO configure (rid,configurations,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid":rid}
	req = update_syncconfiguration_request(ID,apikey,data)
	check(req,401)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_query = """Delete from configure where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (uid, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()
	sql_delete_query = """Delete from users where uid = %s"""
        cur.execute(sql_delete_query, (uid, ))
        connection.commit()


def delete_syncconfiguration_no_ridandcid(ID,apikey):
	data = {}
	req = delete_syncconfiguration_request(ID,apikey,data)
	check(req,400)

def delete_syncconfiguration_no_cid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"volume":80})
	cur.execute("""INSERT INTO configure (rid,configurations,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid":rid}
	req = delete_syncconfiguration_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def delete_syncconfiguration_no_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"volume":80})
	cur.execute("""INSERT INTO configure (rid,configurations,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"cid":cid}
	req = delete_syncconfiguration_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def delete_syncconfiguration_validcase(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"volume":80})
	cur.execute("""INSERT INTO configure (rid,configurations,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid":rid}
	req = delete_syncconfiguration_request(ID,apikey,data)
	check(req,200)	
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def delete_syncconfiguration_valid_cid_invalid_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"volume":80})
	cur.execute("""INSERT INTO configure (rid,configurations,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)]),"cid":cid}
	req = delete_syncconfiguration_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def delete_syncconfiguration_valid_rid_invalid_cid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"volume":80})
	cur.execute("""INSERT INTO configure (rid,configurations,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid":rid,"cid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])}
	req = delete_syncconfiguration_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def delete_syncconfiguration_invalid_cidandrid(ID,apikey):
	data = {"rid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)]),"cid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])}
	req = delete_syncconfiguration_request(ID,apikey,data)
	check(req,400)

def delete_syncconfiguration_not_operation_time(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst+60,rst+120,rst+60,rst+120,"inactive","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority) VALUES(%s,%s,%s)""",(rid,ID,3))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"volume":80})
	cur.execute("""INSERT INTO configure (rid,configurations,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid":rid}
	req = delete_syncconfiguration_request(ID,apikey,data)
	check(req,400)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_query = """Delete from configure where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()



def create_syncwrite_validcase(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid" : rid, "content": {"message":"welcome"}}
	req = create_syncwrite_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def create_syncwrite_already_written(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"message":"welcome"})
	cur.execute("""INSERT INTO write_op (rid,content,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid" : rid, "content": {"message":"welcome"}}
	req = create_syncwrite_request(ID,apikey,data)
	check(req,405)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def create_syncwrite_valid_did(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid" : rid, "content": {"message":"welcome"},"id":[device]}
	req = create_syncwrite_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def create_syncwrite_no_content(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid" : rid}
	req = create_syncwrite_request(ID,apikey,data)
	check(req,400)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def create_syncwrite_unreserved_did(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	d2 = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(d2,'public'))
	connection.commit()
	data = {"rid" : rid,"id":[d2], "content": {"message":"welcome"}}
	req = create_syncwrite_request(ID,apikey,data)
	check(req,400)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (d2, ))
        connection.commit()

def create_syncwrite_invalid_did(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid" : rid,"id":["".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])], "content": {"message":"welcome"}}
	req = create_syncwrite_request(ID,apikey,data)
	check(req,400)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()
	
def create_syncwrite_no_ridorcid(ID,apikey):
	data = {"content": {"message":"welcome"}}
	req = create_syncwrite_request(ID,apikey,data)
	check(req,400)

def create_syncwrite_no_cid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid":rid,"content": {"message":"welcome"},"id":[device]}
	req = create_syncwrite_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def create_syncwrite_no_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid	
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"cid":cid,"content": {"message":"welcome"}}
	req = create_syncwrite_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def create_syncwrite_invalid_cidandrid(ID,apikey):
	data = {"rid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)]),"cid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)]),"content": {"message":"welcome"}}
	req = create_syncwrite_request(ID,apikey,data)
	check(req,400)

def create_syncwrite_valid_rid_invalid_cid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid":rid,"cid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)]),"content": {"message":"welcome"}}
	req = create_syncwrite_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def create_syncwrite_valid_cid_invalid_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)]),"cid":cid,"content": {"message":"welcome"}}
	req = create_syncwrite_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def create_syncwrite_someoneelse_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(25)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	uid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	apikey = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(32)])
	salt = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	has = generate_password_hash(uid + salt + apikey)
	cur.execute("""INSERT INTO users (uid,salt,hash,type) VALUES(%s,%s,%s,%s)""",(uid,salt,has,"user"))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	gid = uid+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,uid,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,uid,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid":rid,"content": {"message":"welcome"}}
	req = create_syncwrite_request(ID,apikey,data)
	check(req,401)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (uid, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()
	sql_delete_query = """Delete from users where uid = %s"""
        cur.execute(sql_delete_query, (uid, ))
        connection.commit()

def create_syncwrite_not_operation_time(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst+60,rst+120,rst+60,rst+120,"inactive","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority) VALUES(%s,%s,%s)""",(rid,ID,3))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid":rid,"content": {"message":"welcome"}}
	req = create_syncwrite_request(ID,apikey,data)
	check(req,400)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()
	


def update_syncwrite_no_content(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"message":"welcome"})
	cur.execute("""INSERT INTO write_op (rid,content,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid" : rid}
	req = update_syncwrite_request(ID,apikey,data)
	check(req,400)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def update_syncwrite_someoneelse_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(25)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	uid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	apikey = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(32)])
	salt = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	has = generate_password_hash(uid + salt + apikey)
	cur.execute("""INSERT INTO users (uid,salt,hash,type) VALUES(%s,%s,%s,%s)""",(uid,salt,has,"user"))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	gid = uid+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,uid,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,uid,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid":rid,"content": {"message":"welcome"}}
	req = update_syncwrite_request(ID,apikey,data)
	check(req,401)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (uid, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()
	sql_delete_query = """Delete from users where uid = %s"""
        cur.execute(sql_delete_query, (uid, ))
        connection.commit()
	
def update_syncwrite_no_ridandcid(ID,apikey):
	data = {"content": {"message":"welcome"}}
	req = update_syncwrite_request(ID,apikey,data)
	check(req,400)

def update_syncwrite_no_cid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"message":"welcome"})
	cur.execute("""INSERT INTO write_op (rid,content,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid":rid,"content": {"message":"welcome"},"id":[device]}
	req = update_syncwrite_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def update_syncwrite_no_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"message":"welcome"})
	cur.execute("""INSERT INTO write_op (rid,content,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"cid":cid,"content": {"message":"welcome"},"id":[device]}
	req = update_syncwrite_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def update_syncwrite_validcase(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"message":"welcome"})
	cur.execute("""INSERT INTO write_op (rid,content,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid" : rid, "content": {"message":"welcome"}}
	req = update_syncwrite_request(ID,apikey,data)
	check(req,200)	
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def update_syncwrite_valid_cid_invalid_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"message":"welcome"})
	cur.execute("""INSERT INTO write_op (rid,content,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)]),"cid":cid,"content": {"message":"welcome"}}
	req = update_syncwrite_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def update_syncwrite_valid_rid_invalid_cid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"message":"welcome"})
	cur.execute("""INSERT INTO write_op (rid,content,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid":rid,"cid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)]),"content": {"message":"welcome"}}
	req = update_syncwrite_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def update_syncwrite_invalid_cidandrid(ID,apikey):
	data = {"rid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)]),"cid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)]),"content": {"message":"welcome"}}
	req = update_syncwrite_request(ID,apikey,data)
	check(req,400)

def update_syncwrite_not_operation_time(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"inactive","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority) VALUES(%s,%s,%s)""",(rid,ID,3))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"message":"welcome"})
	cur.execute("""INSERT INTO write_op (rid,content,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid":rid,"content": {"message":"welcome"}}
	req = update_syncwrite_request(ID,apikey,data)
	check(req,400)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()



def delete_syncwrite_no_content_written(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid" : rid}
	req = delete_syncwrite_request(ID,apikey,data)
	check(req,404)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def delete_syncwrite_someoneelse_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(25)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	uid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	apikey = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(32)])
	salt = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	has = generate_password_hash(uid + salt + apikey)
	cur.execute("""INSERT INTO users (uid,salt,hash,type) VALUES(%s,%s,%s,%s)""",(uid,salt,has,"user"))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	gid = uid+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,uid,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,uid,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid":rid}
	req = update_syncwrite_request(ID,apikey,data)
	check(req,401)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (uid, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()
	sql_delete_query = """Delete from users where uid = %s"""
        cur.execute(sql_delete_query, (uid, ))
        connection.commit()

def delete_syncwrite_no_ridandcid(ID,apikey):
	data = {"configurations": {"volume":80}}
	req = delete_syncwrite_request(ID,apikey,data)
	check(req,400)

def delete_syncwrite_no_cid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"message":"welcome"})
	cur.execute("""INSERT INTO write_op (rid,content,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid":rid}
	req = delete_syncwrite_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def delete_syncwrite_no_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"message":"welcome"})
	cur.execute("""INSERT INTO write_op (rid,content,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"cid":cid}
	req = delete_syncwrite_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def delete_syncwrite_validcase(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"message":"welcome"})
	cur.execute("""INSERT INTO write_op (rid,content,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid" : rid}
	req = delete_syncwrite_request(ID,apikey,data)
	check(req,200)	
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def delete_syncwrite_valid_cid_invalid_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"message":"welcome"})
	cur.execute("""INSERT INTO write_op (rid,content,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)]),"cid":cid}
	req = delete_syncwrite_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def delete_syncwrite_valid_rid_invalid_cid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority,cid) VALUES(%s,%s,%s,%s)""",(rid,ID,3,cid))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"message":"welcome"})
	cur.execute("""INSERT INTO write_op (rid,content,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid":rid,"cid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])}
	req = delete_syncwrite_request(ID,apikey,data)
	check(req,200)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def delete_syncwrite_invalid_cidandrid(ID,apikey):
	data = {"rid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)]),"cid":"".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])}
	req = delete_syncwrite_request(ID,apikey,data)
	check(req,400)

def delete_syncwrite_not_operation_time(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(20)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())+60
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+120,rst,rst+120,"inactive","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority) VALUES(%s,%s,%s)""",(rid,ID,3))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"message":"welcome"})
	cur.execute("""INSERT INTO write_op (rid,content,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'sync',json.dumps([device])))
	connection.commit()
	data = {"rid":rid}
	req = delete_syncwrite_request(ID,apikey,data)
	check(req,400)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()



def create_asyncconfiguration_validcase(ID,apikey):
	query = """select * from reservations_info where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	data = {"rid" : rid, "configurations": {"volume":80}}
	req = create_asyncconfiguration_request(ID,apikey,data)
	check(req,200)

def create_asyncconfiguration_valid_did(ID,apikey):
	query = """select * from reservations_info where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	query = """select * from device_state where rid = %s"""
    	cur.execute(query,(rid, ))
    	record = cur.fetchone()
	
	for did in record[1]:
		data = {"rid" : rid, "configurations": {"volume":80},"id":did}
		req = create_asyncconfiguration_request(ID,apikey,data)
		check(req,200)

def create_asyncconfiguration_no_configurations(ID,apikey):
	query = """select * from reservations_info where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	data = {"rid" : rid}
	req = create_asyncconfiguration_request(ID,apikey,data)
	check(req,400)

def create_asyncconfiguration_invalid_did(ID,apikey):
	query = """select * from reservations_info where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	data = {"rid" : rid,"id":["".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])], "configurations": {"volume":80}}
	req = create_asyncconfiguration_request(ID,apikey,data)
	check(req,400)

def create_asyncconfiguration_unreserved_did(ID,apikey):
	query = """select * from reservations_info where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	did = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(did,'public'))
	connection.commit()	
	data = {"rid" : rid,"id":[did], "configurations": {"volume":80}}
	req = create_asyncconfiguration_request(ID,apikey,data)
	check(req,400)

def create_asyncconfiguration_no_rid(ID,apikey):
	data = {"configurations": {"volume":80}}
	req = create_asyncconfiguration_request(ID,apikey,data)
	check(req,400)

def create_asyncconfiguration_someoneelse_rid(ID,apikey):
	query = """select * from reservations_info where uid != %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	data = {"rid":rid,"configurations": {"volume":80}}
	req = create_asyncconfiguration_request(ID,apikey,data)
	check(req,400)



def create_asyncwrite_validcase(ID,apikey):
	query = """select * from reservations_info where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	data = {"rid" : rid, "content": {"message":"welcome"}}
	req = create_asyncwrite_request(ID,apikey,data)
	check(req,200)

def create_asyncwrite_valid_did(ID,apikey):
	query = """select * from reservations_info where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	query = """select * from device_state where rid = %s"""
    	cur.execute(query,(rid, ))
    	record = cur.fetchone()
	for did in record[1]:
		data = {"rid" : rid, "content": {"message":"welcome"},"id":did}
		req = create_asyncwrite_request(ID,apikey,data)
		check(req,200)

def create_asyncwrite_no_content(ID,apikey):
	query = """select * from reservations_info where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	data = {"rid" : rid}
	req = create_asyncwrite_request(ID,apikey,data)
	check(req,400)

def create_asyncwrite_unreserved_did(ID,apikey):
	query = """select * from reservations_info where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	did = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(did,'public'))
	connection.commit()	
	data = {"rid" : rid,"id":[did], "content": {"message":"welcome"}}
	req = create_asyncwrite_request(ID,apikey,data)
	check(req,400)

def create_asyncwrite_invalid_did(ID,apikey):
	query = """select * from reservations_info where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	data = {"rid" : rid,"id":["".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])], "content": {"message":"welcome"}}
	req = create_asyncwrite_request(ID,apikey,data)
	check(req,400)

def create_asyncwrite_no_rid(ID,apikey):
	data = {"content": {"message":"welcome"}}
	req = create_asyncwrite_request(ID,apikey,data)
	check(req,400)

def create_asyncwrite_someoneelse_rid(ID,apikey):
	query = """select * from reservations_info where uid != %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	data = {"rid":rid,"content": {"message":"welcome"},"id":["asdscd3213"]}
	req = create_asyncwrite_request(ID,apikey,data)
	check(req,400)



def device_status_validcase_without_did(ID,apikey):
	query = """select * from configure as c, reservations_info as r where r.uid = %s and r.rid = c.rid"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	data = {"rid" : record[0]}
	req = device_status_request(ID,apikey,data)
	check(req,200)

def device_status_validcase_with_did(ID,apikey):
	query = """select * from device_state as s, configure as c, reservations_info as r where r.uid = %s and r.rid = s.rid and c.rid = r.rid"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	for did in record[1]:
		data = {"rid" : record[0],"did": did}
		req = device_status_request(ID,apikey,data)
		check(req,200)

def device_status_with_invalid_did(ID,apikey):
	query = """select * from configure as c, reservations_info as r where r.uid = %s and c.rid = r.rid"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	did = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	data = {"rid" : record[0],"did": did}
	req = device_status_request(ID,apikey,data)
	check(req,400)
	
def device_status_with_configurations_not_made(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+1200,rst,rst+1200,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority) VALUES(%s,%s,%s)""",(rid,ID,3))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	data = {"rid" : rid}
	req = device_status_request(ID,apikey,data)
	check(req,204)
	delete_query = """Delete from reservations_info where rid = %s"""
        cur.execute(delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
	connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()

def device_status_with_invalid_rid(ID,apikey):
	data = {"rid" : "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])}
	req = device_status_request(ID,apikey,data)
	check(req,400)

def device_status_with_no_rid(ID,apikey):
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	data = {"did":device}
	req = device_status_request(ID,apikey,data)
	check(req,400)
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()



def operational_status_validcase_without_did(ID,apikey):
	query = """select * from reservations_info where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	data = {"rid" : rid}
	req = operational_status_request(ID,apikey,data)
	check(req,200)

def operational_status_validcase_with_did(ID,apikey):
	query = """select * from device_state as s, reservations_info as r where r.uid = %s and r.rid = s.rid"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	for did in record[1]:
		data = {"rid" : record[0],"did": did}
		req = operational_status_request(ID,apikey,data)
		check(req,200)

def operational_status_with_invalid_did(ID,apikey):
	query = """select * from reservations_info where uid = %s"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	rid = record[0]
	did = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(25)])
	data = {"rid" : rid,"did": did}
	req = operational_status_request(ID,apikey,data)
	check(req,400)

def operational_status_with_invalid_rid(ID,apikey):
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	data = {"rid" : rid}
	req = operational_status_request(ID,apikey,data)
	check(req,400)

def operational_status_with_no_rid(ID,apikey):
	query = """select * from devices"""
    	cur.execute(query,(ID, ))
    	record = cur.fetchone()
	did = record[0]
	data = {"did":did}
	req = operational_status_request(ID,apikey,data)
	check(req,400)



def check(response, code):

	assert_exit(response.status_code == code, 'Message = ' + response.text + ' Status code ='+ str(response.status_code))


def assert_exit(condition, error_message):
	try:
        	assert condition
	except AssertionError:
        	print error_message
        	raise


def functional_tests():
	ID = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	apikey = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(32)])
	salt = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	has = generate_password_hash(ID + salt + apikey)
	cur.execute("""INSERT INTO users (uid,salt,hash,type) VALUES(%s,%s,%s,%s)""",(ID,salt,has,"user"))
	connection.commit()
	device = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device,'public'))
	connection.commit()
	gid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	gid = ID+"-"+gid
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid,ID,json.dumps([device])))
	connection.commit()
	ID2 = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	salt = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(5)])
	has = generate_password_hash(ID2 + salt + apikey)
	cur.execute("""INSERT INTO users (uid,salt,hash,type) VALUES(%s,%s,%s,%s)""",(ID2,salt,has,"user"))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid,rst,rst+1200,rst,rst+1200,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority) VALUES(%s,%s,%s)""",(rid,ID,3))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid,json.dumps([device])))
	connection.commit()
	c = json.dumps({"message":"welcome"})
	cur.execute("""INSERT INTO write_op (rid,content,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'async',json.dumps([device])))
	connection.commit()
	c = json.dumps({"volume":80})
	cur.execute("""INSERT INTO configure (rid,configurations,type,id) VALUES(%s,%s,%s,%s)""",(rid,c,'async',json.dumps([device])))
	connection.commit()
	device2 = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(15)])
	cur.execute("""INSERT INTO devices (did,accessibility) VALUES(%s,%s)""",(device2,'public'))
	connection.commit()
	gid2 = ID2+"-"+gid
	gid2 = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO groups (gid,uid,device_list) VALUES(%s,%s,%s)""",(gid2,ID2,json.dumps([device])))
	connection.commit()
	currentDT = datetime.now()
        sdate = str(currentDT.year)+"-"+str(currentDT.month)+"-"+str(currentDT.day)+" "+str(currentDT.hour)+":"+str(currentDT.minute)+":"+str(currentDT.second)
	stime = datetime.strptime(sdate, '%Y-%m-%d %H:%M:%S')
	rst = time.mktime(stime.timetuple())
	rid2 = "".join([random.choice(string.ascii_lowercase + string.digits) for i in range(10)])
	cur.execute("""INSERT INTO reservations (rid,rst,ret,st,et,state,frequency,duration) VALUES(%s,%s,%s,%s,%s,%s,%s,%s)""",(rid2,rst,rst+1200,rst,rst+1200,"active","null",0))
	connection.commit()
	cur.execute("""INSERT INTO reservations_info (rid,uid,priority) VALUES(%s,%s,%s)""",(rid2,ID2,3))
	connection.commit()
	cur.execute("""INSERT INTO device_state (rid,device_list) VALUES(%s,%s)""",(rid2,json.dumps([device])))
	connection.commit()
	

	signup_validcase()
	signup_no_id()
	signup_id_already_existing()
	signup_id_length_exceeded()
	signup_id_not_alphanumeric()

	creategroup_validcase(ID, apikey)
	creategroup_groupname_already_existing(ID, apikey)
	creategroup_no_groupname(ID, apikey)
	creategroup_no_body(ID, apikey)
	creategroup_no_resources(ID, apikey)
	creategroup_admin_resources(ID, apikey)
	creategroup_invalid_resources(ID, apikey)
	create_group_groupname_not_alphanumeric(ID, apikey)
	create_group_groupname_length_exceeded(ID, apikey)

	update_group_validcase(ID,apikey)
	update_group_no_resources(ID,apikey)
	update_group_admin_resources(ID,apikey)
	update_group_invalid_resources(ID,apikey)
	update_group_gid_empty(ID,apikey)
	update_group_someoneelse_gid(ID,apikey)

	delete_group_validcase(ID,apikey)
	delete_group_invalid_gid(ID,apikey)
	delete_group_gid_empty(ID,apikey)

	create_reservation_validcase(ID,apikey)
	create_reservation_frequency_duration_given(ID,apikey)
	create_reservation_duration_exceeds_reservationtime(ID,apikey)
	create_reservation_wrong_datetime_format(ID,apikey)
	create_reservation_someoneelse_gid(ID,apikey)
	create_reservation_no_gid(ID,apikey)
	create_reservation_alreadyreserved(ID,apikey)
	create_reservation_frequencygiven_noduration(ID,apikey)
	create_reservation_invalid_frequency(ID,apikey)
	create_reservation_endtime_before_starttime(ID,apikey)
	create_reservation_starttime_already_passed(ID,apikey)
	create_reservation_no_starttime_noendtime(ID,apikey)
	create_reservation_no_starttime(ID,apikey)
	create_reservation_no_endtime(ID,apikey)

	update_reservation_wrong_datetime_format(ID,apikey)
	update_reservation_invalid_frequency(ID,apikey)
	update_reservation_invalid_rid(ID,apikey)
	update_reservation_someoneelse_rid(ID,apikey)
	update_reservation_starttime_already_passed(ID,apikey)
	
	update_reservation_no_rid(ID,apikey)
	delete_reservation_no_rid(ID,apikey)
	delete_reservation_someoneelse_rid(ID,apikey)
	delete_reservation_invalid_rid(ID,apikey)
	delete_reservation_valid_rid(ID,apikey)
	
	open_channel_validcase(ID,apikey)
	open_channel_no_rid(ID,apikey)
	open_channel_someoneelse_rid(ID,apikey)
	open_channel_invalid_rid(ID,apikey)
	open_channel_outside_reservationtime(ID,apikey)
	open_channel_when_high_priority_task_running(ID,apikey)

	suspend_channel_someoneelse_rid(ID,apikey)
	suspend_channel_valid_rid(ID,apikey)
	suspend_channel_invalid_rid(ID,apikey)
	suspend_channel_without_opening(ID,apikey)
	suspend_channel_valid_rid_invalid_cid(ID,apikey)
	suspend_channel_valid_cid_invalid_rid(ID,apikey)
	suspend_channel_valid_cid(ID,apikey)
	suspend_channel_no_ridandcid(ID,apikey)

	resume_channel_valid_rid(ID,apikey)
	resume_channel_valid_rid_invalid_cid(ID,apikey)
	resume_channel_valid_cid_invalid_rid(ID,apikey)
	resume_channel_valid_cid(ID,apikey)
	resume_channel_someoneelse_rid(ID,apikey)
	resume_channel_invalid_rid(ID,apikey)
	resume_channel_without_opening(ID,apikey)
	resume_channel_without_suspending(ID,apikey)
	resume_channel_no_ridandcid(ID,apikey)

	close_channel_someoneelse_rid(ID,apikey)
	close_channel_valid_rid(ID,apikey)
	close_channel_invalid_rid(ID,apikey)
	close_channel_without_opening(ID,apikey)
	close_channel_valid_rid_invalid_cid(ID,apikey)
	close_channel_valid_cid_invalid_rid(ID,apikey)
	close_channel_valid_cid(ID,apikey)
	close_channel_no_ridandcid(ID,apikey)

	create_syncconfiguration_validcase(ID,apikey)
	create_syncconfiguration_already_configured(ID,apikey)
	create_syncconfiguration_valid_did(ID,apikey)
	create_syncconfiguration_no_configurations(ID,apikey)
	create_syncconfiguration_invalid_did(ID,apikey)
	create_syncconfiguration_invalid_cidandrid(ID,apikey)
	create_syncconfiguration_unreserved_did(ID,apikey)
	create_syncconfiguration_no_ridandcid(ID,apikey)
	create_syncconfiguration_someoneelse_rid(ID,apikey)
	create_syncconfiguration_no_cid(ID,apikey)
	create_syncconfiguration_no_rid(ID,apikey)
	create_syncconfiguration_valid_rid_invalid_cid(ID,apikey)
	create_syncconfiguration_valid_cid_invalid_rid(ID,apikey)
	create_syncconfiguration_not_operation_time(ID,apikey)

	update_syncconfiguration_no_configurations(ID,apikey)
	update_syncconfiguration_no_configurations_made(ID,apikey)
	update_syncconfiguration_someoneelse_rid(ID,apikey)
	update_syncconfiguration_no_ridandcid(ID,apikey)
	update_syncconfiguration_no_cid(ID,apikey)
	update_syncconfiguration_no_rid(ID,apikey)
	update_syncconfiguration_validcase(ID,apikey)
	update_syncconfiguration_valid_cid_invalid_rid(ID,apikey)
	update_syncconfiguration_valid_rid_invalid_cid(ID,apikey)
	update_syncconfiguration_invalid_cidandrid(ID,apikey)
	update_syncconfiguration_not_operation_time(ID,apikey)

	delete_syncconfiguration_no_configurations_made(ID,apikey)
	delete_syncconfiguration_someoneelse_rid(ID,apikey)
	delete_syncconfiguration_no_ridandcid(ID,apikey)
	delete_syncconfiguration_no_rid(ID,apikey)
	delete_syncconfiguration_invalid_cidandrid(ID,apikey)
	delete_syncconfiguration_not_operation_time(ID,apikey)
	delete_syncconfiguration_valid_cid_invalid_rid(ID,apikey)
	delete_syncconfiguration_valid_rid_invalid_cid(ID,apikey)
	delete_syncconfiguration_validcase(ID,apikey)
	delete_syncconfiguration_no_cid(ID,apikey)

	create_syncwrite_no_content(ID,apikey)
	create_syncwrite_unreserved_did(ID,apikey)
	create_syncwrite_invalid_cidandrid(ID,apikey)
	create_syncwrite_invalid_did(ID,apikey)
	create_syncwrite_no_ridorcid(ID,apikey)
	create_syncwrite_validcase(ID,apikey)
	create_syncwrite_already_written(ID,apikey)
	create_syncwrite_valid_did(ID,apikey)
	create_syncwrite_no_cid(ID,apikey)
	create_syncwrite_no_rid(ID,apikey)
	create_syncwrite_valid_rid_invalid_cid(ID,apikey)
	create_syncwrite_valid_cid_invalid_rid(ID,apikey)
	create_syncwrite_someoneelse_rid(ID,apikey)
	create_syncwrite_not_operation_time(ID,apikey)

	update_syncwrite_no_content(ID,apikey)
	update_syncwrite_someoneelse_rid(ID,apikey)
	update_syncwrite_no_ridandcid(ID,apikey)
	update_syncwrite_no_cid(ID,apikey)
	update_syncwrite_no_rid(ID,apikey)
	update_syncwrite_validcase(ID,apikey)
	update_syncwrite_valid_cid_invalid_rid(ID,apikey)
	update_syncwrite_valid_rid_invalid_cid(ID,apikey)
	update_syncwrite_invalid_cidandrid(ID,apikey)
	update_syncwrite_not_operation_time(ID,apikey)

	delete_syncwrite_validcase(ID,apikey)
	delete_syncwrite_valid_cid_invalid_rid(ID,apikey)
	delete_syncwrite_no_rid(ID,apikey)
	delete_syncwrite_no_cid(ID,apikey)
	delete_syncwrite_no_content_written(ID,apikey)
	delete_syncwrite_someoneelse_rid(ID,apikey)
	delete_syncwrite_no_ridandcid(ID,apikey)
	delete_syncwrite_invalid_cidandrid(ID,apikey)
	delete_syncwrite_not_operation_time(ID,apikey)
	delete_syncwrite_valid_rid_invalid_cid(ID,apikey)
	
	create_asyncconfiguration_validcase(ID,apikey)
	create_asyncconfiguration_valid_did(ID,apikey)
	create_asyncconfiguration_no_configurations(ID,apikey)
	create_asyncconfiguration_invalid_did(ID,apikey)
	create_asyncconfiguration_unreserved_did(ID,apikey)
	create_asyncconfiguration_no_rid(ID,apikey)
	create_asyncconfiguration_someoneelse_rid(ID,apikey)

	create_asyncwrite_validcase(ID,apikey)
	create_asyncwrite_valid_did(ID,apikey)
	create_asyncwrite_no_content(ID,apikey)
	create_asyncwrite_unreserved_did(ID,apikey)
	create_asyncwrite_invalid_did(ID,apikey)
	create_asyncwrite_no_rid(ID,apikey)
	create_asyncwrite_someoneelse_rid(ID,apikey)	

	device_status_validcase_without_did(ID,apikey)
	device_status_validcase_with_did(ID,apikey)
	device_status_with_invalid_did(ID,apikey)
	device_status_with_configurations_not_made(ID,apikey)
	device_status_with_invalid_rid(ID,apikey)
	device_status_with_no_rid(ID,apikey)

	operational_status_validcase_without_did(ID,apikey)
	operational_status_validcase_with_did(ID,apikey)
	operational_status_with_invalid_did(ID,apikey)
	operational_status_with_invalid_rid(ID,apikey)
	operational_status_with_no_rid(ID,apikey)
	

	

	sql_delete_query = """Delete from write_op where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_query = """Delete from configure where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	delete_query = """Delete from reservations_info where uid = %s"""
        cur.execute(delete_query, (ID, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device, ))
        connection.commit()
	sql_query = """Delete from users where uid = %s"""
        cur.execute(sql_query, (ID, ))
        connection.commit()
	delete_query = """Delete from reservations_info where uid = %s"""
        cur.execute(delete_query, (ID2, ))
        connection.commit()
	sql_query = """Delete from device_state where rid = %s"""
        cur.execute(sql_query, (rid2, ))
        connection.commit()
	sql_delete_query = """Delete from reservations where rid = %s"""
        cur.execute(sql_delete_query, (rid2, ))
        connection.commit()
	sql_delete_query = """Delete from groups where uid = %s"""
        cur.execute(sql_delete_query, (ID2, ))
        connection.commit()
	sql_query = """Delete from users where uid = %s"""
        cur.execute(sql_query, (ID2, ))
        connection.commit()
	sql_delete_query = """Delete from devices where did = %s"""
        cur.execute(sql_delete_query, (device2, ))
        connection.commit()
	
	print 'all test cases passed'
if __name__ == '__main__':
	
	functional_tests()
