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

def serialop():
    while True:
        sum = 0
        count = ser.inWaiting()  # 位置4
        if count != 0:
            ser.write(str(count))  # 位置7
            ser.write("Recv some data is : ".encode("utf-8"))  # 位置6
            recv = ser.read(count)  # 位置
            #ser.write(str(recv))  # 位置7
            sum = int(recv)
            ser.write(recv)
            ser.write(str(sum)[0:3])
            ser.write("\n")
            ser.flushInput()
        time.sleep(0.1)  # 位置8

def get_temp():
        # 打开文件 
        file = open("/sys/class/thermal/thermal_zone0/temp") 
        # 读取结果，并转换为浮点数 
        temp = float(file.read()) / 1000 
        # 关闭文件 
        file.close() 
        # 向控制台打印结果 
        print("CPU tempurature: %.3f" %temp )
        # 返回温度值
        return temp

        
        
def http_put():
        temperature= get_temp()
        CurTime = datetime.datetime.now()
        url='http://api.heclouds.com/devices/595562605/datapoints'  #你的设备id
        values={'datastreams':[{"id":"temp","datapoints":[{"value":temperature}]}]}#你的数据流名称
        print ("Cur_time:%s" %CurTime.isoformat())
        print ("tempure:%.3f" %temperature)
        jdata = json.dumps(values)
        print jdata
        request = urllib2.Request(url, jdata)
        request.add_header('api-key', APIKEY)
        request.get_method = lambda:'POST'
        request = urllib2.urlopen(request)
        return request.read()

while True:
    print(get_temp())  
    time.sleep(1)
    resp = http_put()
    print "OneNET result:\n %s" %resp
    time.sleep(2)
