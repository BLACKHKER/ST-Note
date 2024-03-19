```python
const uploadProps = {
  name: 'file',
  action: 'https://www.mocky.io/v2/5cc8019d300000980a055e76',
  headers: {
    authorization: 'authorization-text',
  },
  onChange(info) {
    if (info.file.status !== 'uploading') {
      // console.log(info.file, info.fileList);
    }
    if (info.file.status === 'done') {
      message.success(`${info.file.name} file uploaded successfully`);
    } else if (info.file.status === 'error') {
      message.error(`${info.file.name} file upload failed.`);
    }
  },
};
/***************************************/
<Upload {...uploadProps}>
                        <Button icon={<UploadOutlined />} onClick={ (e) => { this.onUploadClickConfig() }}>配置文件导入</Button>
                      </Upload>
        
/***************************************/
onUploadClickConfig(){


    <Upload action="/offline/config" directory>
    <Button icon={<UploadOutlined />}>Upload Directory</Button>
    </Upload>


  }
```

