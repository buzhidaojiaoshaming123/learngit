忽悠故人上心头，回首山河已是秋。
Git is a version control system.
Git is free software.
liujaiqi
ceshiyixia
this is a new beginning
Once again, as a content I want
Creating a new branch is quick.
di fan zhi
Creating a new branch is quick & simple.
NONGFU SPRING
忽有故人上心头，回首山河已是秋。
两处相思同淋雪，此生也算共白头。
#!/usr/bin/env python
# -*- coding:utf-8 -*-
from camera import Camera
from flask import Flask, render_template, Response, jsonify

# 导入 camera
import cv2

app = Flask(__name__)
#Flask类只有一个必须指定的参数，即程序主模块或者包的名字，__name__是系统变量，该变量指的是本py文件的文件名
#app是flask的实例，功能就是接受来自web服务器的请求，
#浏览器将请求给web服务器，web服务器将请求给app ,
#app收到请求，通过路由找到对应的视图函数，然后将请求处理，得到一个响应response
#然后app将响应返回给web服务器，
#web服务器返回给浏览器，
camera = Camera()
#给个定义可以将Camera从camera文件里导入进来

#global全局变量
global cabbage_num
cabbage_num = 1

#GET：http请求方式
@app.route('/', methods=['GET'])
def index():
	return render_template('indexindex.html')

#GET：http请求方式
@app.route('/_stuff', methods = ['GET'])
def stuff():
	global cabbage_num
	return jsonify(num=cabbage_num, reserved=12.84)

def gen(id_cam):
	global cabbage_num
	if(int(id_cam)==0):
		while True:
				frame, cabbage_num = camera.get_frame()
				yield (b'--frame\r\n' b'Content-Type: image/jpeg\r\n\r\n' + frame + b'\r\n')
	else:
		while True:
				frame = camera.get_frame2()
				if frame is None:
						continue
				yield (b'--frame\r\n' b'Content-Type: image/jpeg\r\n\r\n' + frame + b'\r\n')

#<string:id> url中的可变部分，用于声明变量
@app.route('/video_feed/<string:id>/', methods=['GET'])
def video_feed(id):
	return Response(gen(id), mimetype='multipart/x-mixed-replace; boundary=frame')
#mimetype='multipart/x-mixed-replace;处理这种Multipart类型时，会使用当前的块数据替换之前的快数据，把一帧数据大巴成一个块


if __name__ == '__main__':
	app.run(host='0.0.0.0', debug=True, port=5000)
#__name__ == '__main__'是python常用的方法，表示只有直接启动本脚本时候，才用app.run方法
#debug=True：如果设置了:attr:`debug '标志，服务器将自动重新加载用于代码更改，并在发生异常时显示调试器


