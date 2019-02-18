# 构建fastdfs镜像的脚本

## 构建步骤 1：

### 将安装包及文件拷贝到统一目录下，运行命令
### XXX为构建的镜像名

    docker build -t wei_fastdfs --rm=true .

## 构建步骤 2：

### 创建tracker
### TRACKER_SERVER ： tracker服务端ip
### TR_NGX_PORT    ： tracker服务端上运行的nginx端口
### ST_NGX_PORT    ： storage服务端上运行的nginx端口
### 62e919b7efc1   :  镜像id
### t1             ： tracker服务端名称

    #docker run -ti -d --name t1 -v ~/tracker_data:/fastdfs/tracker/data --net=host -e TRACKER_SERVER=192.168.1.81:22122 -e TR_NGX_PORT=7090 -e ST_NGX_PORT=7050 62e919b7efc1 tracker
    
    --- 阿里云的机器上传图片超时
    docker run -ti -d --name t1 -v ~/tracker_data:/fastdfs/tracker/data --net=host -e TRACKER_SERVER=120.55.162.42:22122 -e TR_NGX_PORT=7090 -e  ST_NGX_PORT=7050 0cca5a3646b2 tracker

    docker run -ti -d --name t1 -v ~/tracker_data:/fastdfs/tracker/data --net=host -e TRACKER_SERVER=10.4.65.226:22122 -e TR_NGX_PORT=7090 -e ST_NGX_PORT=7050 3e5848cfc96e tracker

### 创建storage
### GROUP_NAME ：创建的storage属于哪个group，不填写则为1      例： GROUP_NAME=group2
### 其他参数同上

    #docker run -ti --name s1 -v ~/storage_data:/fastdfs/storage/data -v ~/store_path:/fastdfs/store_path --net=host -e TRACKER_SERVER=192.168.1.81:22122 -e TR_NGX_PORT=7090 -e ST_NGX_PORT=7050 62e919b7efc1 storage

    --- 阿里云的机器上传图片超时
    docker run -ti --name s1 -v ~/storage_data:/fastdfs/storage/data -v ~/store_path:/fastdfs/store_path --net=host -e TRACKER_SERVER=120.55.162.42:22122 -e TR_NGX_PORT=7090 -e ST_NGX_PORT=7050 0cca5a3646b2  storage


    docker run -ti --name s1 -v ~/storage_data:/fastdfs/storage/data -v ~/store_path:/fastdfs/store_path --net=host -e TRACKER_SERVER=10.4.65.226:22122 -e TR_NGX_PORT=7090 -e ST_NGX_PORT=7050 3e5848cfc96e  storage

# 构建结束


# tip
## 查看集群状态

    fdfs_monitor /etc/fdfs/client.conf

## 测试上传文件
 
    /usr/local/bin/fdfs_test /etc/fdfs/client.conf upload anti-steal.jpg 

## nginx.conf 目录

    /usr/local/nginx/nginx.conf 

