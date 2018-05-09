# python-PM2.5-
利用python爬取PM2.5数据
======================

PM2.5数据来源于http://www.86pm25.com/city/beijing.html，数据更新时间为一小时一次，历史数据网站上没有，因此无法获取，只能从当前时间向后爬取

1.导入库
-------
import time
from threading import Timer 
import pandas as pd 
import numpy as np

2.爬虫函数
---------

def delayrun():
	while True:
		file_time=time.strftime('%Y-%m-%d-%H',time.localtime(time.time())) <br>
		file_name='C:/Users/SQ/Desktop/'+file_time+'-PM.csv' <br>

		data=pd.read_html('http://www.86pm25.com/city/beijing.html')[0] <br>
		data=data.ix[:,[0,1,2,4,5]].copy() <br>
		data.ix[:,3]=data.ix[:,3].str.replace('μg/m³','') <br>
		data.ix[:,4]=data.ix[:,4].str.replace('μg/m³','') <br>
		data.to_csv(file_name) <br>


3.时间控件
---------

    间隔时间，设置为3600秒即1小时
timer_interval=3600 <br>
t=Timer(timer_interval,delayrun)   <br>
t.start()  <br>
