## 本地运行

1. 克隆仓库并进入目录

```sh
git clone https://github.com/your_username/telegram_media_downloader.git
cd telegram_media_downloader
```

2. 准备配置文件并编辑

```sh
cp config.yaml.example config.yaml
vi config.yaml
```

3. 修改 docker-compose.yaml 使用本地构建并删除远程 image

编辑 `docker-compose.yaml` 文件，将 `image` 字段删除，添加 `build: .`，示例如下：

```yaml
services:
  telegram_media_downloader:
    build: .
    # image: tangyoha/telegram_media_downloader:latest  # 删除此行
    volumes:
      - ./config.yaml:/app/config.yaml
      - ./data.yaml:/app/data.yaml
      - ./log:/app/log
    ports:
      - "5000:5000"
```

4. 构建 Docker 镜像

```sh
docker-compose build
```

5. 第一次运行前台授权

```sh
docker-compose run --rm telegram_media_downloader
```

运行后，输入手机号码和验证码完成授权，完成后按 `Ctrl + C` 退出。

6. 后续后台启动

```sh
docker-compose up -d
```

---

### 注意事项

- 第一次运行必须完成前台授权，否则机器人无法正常工作。
- 每次源码修改后需重新构建镜像（`docker-compose build`），以确保修改生效。
