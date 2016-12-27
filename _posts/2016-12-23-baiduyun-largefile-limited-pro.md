---
layout: post
title: 让百度网盘支持大文件上传（续）
date: 2016-12-23 17:38:16 
category: "软件"
comment: true
---

在[让百度网盘支持大文件上传][1]中提到，百度PCS提供了两种上传方式的REST API，一种是普通上传方式，另一种是分片上传。由于官方文档上写了“普通上传方式只支持最大2GB的文件”，于是选择了分片上传API，这样就很好的解决了大文件上传受限的问题。

[1]: (https://bo-huang.github.io/%E8%BD%AF%E4%BB%B6/2016/12/20/baiduyun-largefile-limited.html)

其实官方文档上还有第三种上传方式: **秒传**，但当时想当然的认为这种上传方式肯定也只支持单文件2GB大小，于是就没有考虑它。

就在刚才,好奇的试了一下秒传API，并还是用超过4GB的系统安装文件进行上传测试，结果成功了！！

于是就改进了之前写的代码，添加了秒传接口，接口详情见[官方文档][2]。

[2]: http://developer.baidu.com/wiki/index.php?title=docs/pcs/rest/file_data_apis_list#.E7.A7.92.E4.BC.A0.E6.96.87.E4.BB.B6 "repid upload"

秒传其实就是上传前先计算文件md5，然后与百度云上已经存在的文件的md5值进行比较，如果存在，则不用重复上传；但如果百度云上没有该文件，那么还是需要用分片上传方式。

解决方式：

```c#

private void Upload()
{
    uploadButton.Enabled = false;
    for (int i = 0; i < files.Count;++i )
    {
        string file = files[i];
        progressBar.Value = 0;
        progressBar.Maximum = 100;
        statusLabel.Text = "computing……";
        bpcs.progressEvent = new BPCS.ProgressEventHander(Progress);
        //先尝试利用秒传
        //如果上传失败，很有可能是百度云上没有找到相同的文件
        //这个时候用普通方式上传
        bool ok = bpcs.RapidUpload(file);
        if(!ok)
        {    
            //普通方式上传
            statusLabel.Text = "0%";
            ok = bpcs.Upload(file);
        }
        if (!ok)
            MessageBox.Show(string.Format("{0} upload failed", System.IO.Path.GetFileName(file)));
        DeleteListItem(file);
    }
    files.Clear();
    uploadButton.Enabled = true;
}

```

#### 下载

项目地址：<https://github.com/bo-huang/bpcs>     

[软件传送门][3]

[3]: https://github.com/bo-huang/bpcs_release
