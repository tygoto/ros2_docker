# dockerでros2の実行環境を構築

### 1. 必要なファイルを取得

```bash
$ git clone https://github.com/tygoto/ros2_docker.git
$ cd ros2_docker
```

### 2. ros2 dashingのDockerイメージを作成

```bash
$ docker build --tag ros2:dashing ros2
```

### 3. turtulebotのDockerイメージを作成

```bash
$ docker build --tag turtlebot3 turtlebot3
```

### 4. コンテナを起動

```bash
$ xhost local:
$ docker-compose up
```

### 5. コンテナに入る
```bash
$ docker exec -it <コンテナID> bash
```

### 6. コンテナの停止，その他の終了処理
```bash
<Ctrl+C>
$ docker-compose down
$ xhost -local:
```
