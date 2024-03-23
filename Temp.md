##### 后端Python代码

```python
import uvicorn
import os
from fastapi import FastAPI, File, UploadFile
from fastapi.middleware.cors import CORSMiddleware
from typing import Union
from pydantic import BaseModel

app = FastAPI()

# 跨域资源共享
origins = [
    "*",
]

@app.post('/offline/config')
async def upload_config_data(file: UploadFile = File(...)):
    # 文件名
    fName = file.filename

    # 保存路径
    savePath = r'C:\Upload'

    print('调用接口/offline/config')

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

if __name__ == '__main__':
    uvicorn.run(app='DPS20230407:app', host="0.0.0.0", port=8081, reload=True)
```



##### 控制台输出

```shell
D:\Python\python.exe C:\Users\BHKDOS\Desktop\PythonRevzoneProject\DPS20231227.py 
INFO:     Will watch for changes in these directories: ['C:\\Users\\BHKDOS\\Desktop\\PythonRevzoneProject']
INFO:     Uvicorn running on http://0.0.0.0:8081 (Press CTRL+C to quit)
INFO:     Started reloader process [5508] using StatReload
INFO:     Started server process [30596]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
INFO:     127.0.0.1:57517 - "OPTIONS /offline/config HTTP/1.1" 200 OK
INFO:     127.0.0.1:57517 - "POST /offline/config HTTP/1.1" 200 O
```

