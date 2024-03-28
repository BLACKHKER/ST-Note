A.Py

```python
import uvicorn
import os
import logging
from fastapi import FastAPI, File, UploadFile
from fastapi.middleware.cors import CORSMiddleware
from typing import Union
from pydantic import BaseModel

logging.basicConfig(level=logging.INFO)

app = FastAPI()

# 跨域资源共享
origins = [
    "*",
]

app.add_middleware(
    CORSMiddleware,
    allow_origins=origins,
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)


class s1ap_parameter_online(BaseModel):
    num: Union[int, None] = None
    start_time: Union[str, None] = None
    end_time: Union[str, None] = None


class s1ap_parameter_offline(BaseModel):
    num: Union[int, None] = None
    start_time: Union[str, None] = None
    end_time: Union[str, None] = None


@app.post('/online/s1ap/')
async def get_s1ap_data(s1ap_item: s1ap_parameter_online):
    import pymongo
    from urllib import parse

    username = parse.quote_plus('LTE-M')  # 对用户名进行编码
    password = parse.quote_plus('s1ap')  # 对密码进行编码
    host = "127.0.0.1"
    port = "27017"
    mongo = pymongo.MongoClient('mongodb://%s:%s@%s:%s/admin' % (username, password, host, port))

    database = mongo["LTE_online"]
    s1ap_collection = database["s1ap"]

    num = s1ap_item.num
    start_time = s1ap_item.start_time
    end_time = s1ap_item.end_time

    res = []
    if (num == 0):
        for data in s1ap_collection.find({"frame.frame_time": {"$gte": start_time, "$lte": end_time}}, {'_id': 0}).sort(
                [('frame.frame_time', pymongo.DESCENDING), ('frame.frame_number', pymongo.DESCENDING)]):
            res.append(data)
    else:
        for data in s1ap_collection.find({}, {"_id": 0}).sort(
                [('frame.frame_time', pymongo.DESCENDING), ('frame.frame_number', pymongo.DESCENDING)]).limit(num):
            res.append(data)
    res.reverse()
    return (res)


@app.get('/online/s1ap_element')
async def get_s1ap_element_data():
    import pymongo
    from urllib import parse

    username = parse.quote_plus('LTE-M')  # 对用户名进行编码
    password = parse.quote_plus('s1ap')  # 对密码进行编码
    host = "127.0.0.1"
    port = "27017"
    mongo = pymongo.MongoClient('mongodb://%s:%s@%s:%s/admin' % (username, password, host, port))

    database = mongo["LTE_online"]
    s1ap_element_collection = database["s1ap_element"]

    # num = s1ap_item.num
    # start_time = s1ap_item.start_time
    # end_time = s1ap_item.end_time

    res = []

    for data in s1ap_element_collection.find({}, {"_id": 0}).sort(
            [('frame_time', pymongo.DESCENDING), ('frame_number', pymongo.DESCENDING)]).limit(100):
        res.append(data)
    res.reverse()
    return (res)


@app.get('/online/zbtc')
async def get_zbtc_data():
    import pymongo
    from urllib import parse

    username = parse.quote_plus('LTE-M')  # 对用户名进行编码
    password = parse.quote_plus('s1ap')  # 对密码进行编码
    host = "127.0.0.1"
    port = "27017"
    mongo = pymongo.MongoClient('mongodb://%s:%s@%s:%s/admin' % (username, password, host, port))

    database = mongo["LTE_online"]
    s1ap_element_collection = database["zbtc"]

    # num = s1ap_item.num
    # start_time = s1ap_item.start_time
    # end_time = s1ap_item.end_time

    res = []

    for data in s1ap_element_collection.find({}, {"_id": 0}).sort(
            [('frame_time', pymongo.DESCENDING), ('frame_number', pymongo.DESCENDING)]).limit(100):
        res.append(data)
    res.reverse()
    return (res)


@app.get('/online/error_zbtc')
async def get_error_zbtc_data():
    import pymongo
    from urllib import parse

    username = parse.quote_plus('LTE-M')  # 对用户名进行编码
    password = parse.quote_plus('s1ap')  # 对密码进行编码
    host = "127.0.0.1"
    port = "27017"
    mongo = pymongo.MongoClient('mongodb://%s:%s@%s:%s/admin' % (username, password, host, port))

    database = mongo["LTE_online"]
    s1ap_element_collection = database["error_zbtc"]

    # num = s1ap_item.num
    # start_time = s1ap_item.start_time
    # end_time = s1ap_item.end_time

    res = []

    for data in s1ap_element_collection.find({}, {"_id": 0}).sort([('_id', pymongo.DESCENDING)]).limit(100):
        res.append(data)
    res.reverse()
    return (res)


@app.get('/online/status')
async def get_status_data():
    import pymongo
    from urllib import parse

    username = parse.quote_plus('LTE-M')  # 对用户名进行编码
    password = parse.quote_plus('s1ap')  # 对密码进行编码
    database = "LTE_online"  # 数据库名称
    host = "127.0.0.1"
    port = "27017"
    mongo = pymongo.MongoClient('mongodb://%s:%s@%s:%s/admin' % (username, password, host, port))

    database = mongo[database]

    status_collection = database["status"]

    for data in status_collection.find({}, {"_id": 0}).sort("_id", pymongo.DESCENDING).limit(1):
        res = data
    return (res)


@app.post('/offline/s1ap/')
async def get_s1ap_data(s1ap_item: s1ap_parameter_offline):
    import pymongo
    from urllib import parse

    username = parse.quote_plus('LTE-M')  # 对用户名进行编码
    password = parse.quote_plus('s1ap')  # 对密码进行编码
    host = "127.0.0.1"
    port = "27017"
    mongo = pymongo.MongoClient('mongodb://%s:%s@%s:%s/admin' % (username, password, host, port))

    database = mongo["LTE_offline"]
    s1ap_collection = database["s1ap"]

    num = s1ap_item.num
    start_time = s1ap_item.start_time
    end_time = s1ap_item.end_time

    res = []
    if (num == 0):
        for data in s1ap_collection.find({"frame.frame_time": {"$gte": start_time, "$lte": end_time}}, {'_id': 0}).sort(
                [('frame.frame_time', pymongo.DESCENDING), ('frame.frame_number', pymongo.DESCENDING)]):
            res.append(data)
    else:
        for data in s1ap_collection.find({}, {"_id": 0}).sort(
                [('frame.frame_time', pymongo.DESCENDING), ('frame.frame_number', pymongo.DESCENDING)]).limit(num):
            res.append(data)
    res.reverse()
    return (res)


@app.get('/offline/s1ap_element')
async def get_s1ap_element_data():
    import pymongo
    from urllib import parse

    username = parse.quote_plus('LTE-M')  # 对用户名进行编码
    password = parse.quote_plus('s1ap')  # 对密码进行编码
    host = "127.0.0.1"
    port = "27017"
    mongo = pymongo.MongoClient('mongodb://%s:%s@%s:%s/admin' % (username, password, host, port))

    database = mongo["LTE_offline"]
    s1ap_element_collection = database["s1ap_element"]

    # num = s1ap_item.num
    # start_time = s1ap_item.start_time
    # end_time = s1ap_item.end_time

    res = []

    for data in s1ap_element_collection.find({}, {"_id": 0}).sort(
            [('frame_time', pymongo.DESCENDING), ('frame_number', pymongo.DESCENDING)]).limit(100):
        res.append(data)
    res.reverse()
    return (res)


@app.get('/offline/zbtc')
async def get_zbtc_data():
    import pymongo
    from urllib import parse

    username = parse.quote_plus('LTE-M')  # 对用户名进行编码
    password = parse.quote_plus('s1ap')  # 对密码进行编码
    host = "127.0.0.1"
    port = "27017"
    mongo = pymongo.MongoClient('mongodb://%s:%s@%s:%s/admin' % (username, password, host, port))

    database = mongo["LTE_offline"]
    s1ap_element_collection = database["zbtc"]

    # num = s1ap_item.num
    # start_time = s1ap_item.start_time
    # end_time = s1ap_item.end_time

    res = []

    for data in s1ap_element_collection.find({}, {"_id": 0}).sort(
            [('frame_time', pymongo.DESCENDING), ('frame_number', pymongo.DESCENDING)]).limit(100):
        res.append(data)
    res.reverse()
    return (res)


@app.get('/offline/error_zbtc')
async def get_error_zbtc_data():
    import pymongo
    from urllib import parse

    username = parse.quote_plus('LTE-M')  # 对用户名进行编码
    password = parse.quote_plus('s1ap')  # 对密码进行编码
    host = "127.0.0.1"
    port = "27017"
    mongo = pymongo.MongoClient('mongodb://%s:%s@%s:%s/admin' % (username, password, host, port))

    database = mongo["LTE_offline"]
    s1ap_element_collection = database["error_zbtc"]

    # num = s1ap_item.num
    # start_time = s1ap_item.start_time
    # end_time = s1ap_item.end_time

    res = []

    for data in s1ap_element_collection.find({}, {"_id": 0}).sort([('_id', pymongo.DESCENDING)]).limit(100):
        res.append(data)
    res.reverse()
    return (res)


@app.get('/offline/status')
async def get_status_data():
    import pymongo
    from urllib import parse

    username = parse.quote_plus('LTE-M')  # 对用户名进行编码
    password = parse.quote_plus('s1ap')  # 对密码进行编码
    database = "LTE_offline"  # 数据库名称
    host = "127.0.0.1"
    port = "27017"
    mongo = pymongo.MongoClient('mongodb://%s:%s@%s:%s/admin' % (username, password, host, port))

    database = mongo[database]

    status_collection = database["status"]

    for data in status_collection.find({}, {"_id": 0}).sort("_id", pymongo.DESCENDING).limit(1):
        res = data
    return (res)


@app.post('/offline/config')
async def upload_config_data(file: UploadFile = File(...)):
    print("===============================")
    # 文件名
    fName = file.filename

    # 保存路径
    savePath = r'D:\Upload'

    # 获取根日志记录器
    logger = logging.getLogger()
    if not logger.handlers:
        print("日志记录器未激活")
    else:
        print("日志记录器已激活")

    logging.info('调用接口/offline/config')

    # 路径校验
    if not os.path.exists(savePath):
        os.mkdir(savePath)

    # 组装完整路径
    filePath = os.path.join(savePath, fName)

    # 异常处理
    try:
        # 获取文件的二进制流，并行写入
        with open(filePath, 'wb') as f:
            fileData = await file.read()
            f.write(fileData)
    except:
        return ("配置文件上传失败");

    return ("配置文件上传成功")


@app.post('/offline/file')
async def upload_file_data():
    return ("数据文件上传成功")


if __name__ == '__main__':
    uvicorn.run(app='DPS20230407:app', host="0.0.0.0", port=8081, reload=True, log_level="debug")
```

B.py

```python

```

