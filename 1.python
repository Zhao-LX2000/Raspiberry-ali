#coding:utf-8
import subprocess
import os
import glob
import time
import serial
import urllib2
import json
import time
import datetime

APIKEY = '1FHP56uxeFRdnpx7m2XAgaHpCtI='  #你的APIKEY
ser = serial.Serial("/dev/ttyAMA0", 115200)  # 位置1
ser.flushInput()  # 位置2
ser.write("begin".encode("utf-8"))  # 位置3

        
def http_put():
    temperature = recv[0:4]
    #print ("tempure:%.3s" %temperature)
    temperature = float(temperature)  
    CurTime = datetime.datetime.now()
    url='http://api.heclouds.com/devices/595562605/datapoints'  #你的设备id
    values={'datastreams':[{"id":"temp","datapoints":[{"value":temperature}]}]}#你的数据流名称
    print ("Cur_time:%s" %CurTime.isoformat())
    print ("temperature:%.3f" %temperature)
    jdata = json.dumps(values)
    print jdata
    request = urllib2.Request(url, jdata)
    request.add_header('api-key', APIKEY)
    request.get_method = lambda:'POST'
    request = urllib2.urlopen(request)
    return request.read()

def http_put2():
    humidity = recv[5:7]
    humidity = int(humidity)  
    CurTime = datetime.datetime.now()
    url='http://api.heclouds.com/devices/595562605/datapoints'  #你的设备id
    values={'datastreams':[{"id":"hum","datapoints":[{"value":humidity}]}]}#你的数据流名称
    print ("Cur_time:%s" %CurTime.isoformat())
    print ("humidity:%.0f" %humidity)
    jdata = json.dumps(values)
    print jdata
    request = urllib2.Request(url, jdata)
    request.add_header('api-key', APIKEY)
    request.get_method = lambda:'POST'
    request = urllib2.urlopen(request)
    return request.read()
while True:
    sum = 0
    count = ser.inWaiting()  # 位置4
    if count != 0:
        recv = ser.read(count)  # 位置
        
        time.sleep(1)
        resp = http_put()
        resp = http_put2()
        print "OneNET result:\n %s" %resp
        ser.flushInput()
        time.sleep(2)
