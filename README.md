# dockerでros2の実行環境を構築

### 1. ros2 dashingのコンテナイメージを作成

```bash
$ cd ros2
$ docker build --tag ros2:dashing .
```

### 2. turtulebotのコンテナイメージを作成

```bash
$ cd turtlebot3
$ docker build --tag turtlebot3 .
```

### 3. コンテナを起動

```bash
$ docker-compose up
```

- 終了する場合
```bash
$ docker-compose down
```

### 4. コンテナに入る
```bash
$ docker exec -it <コンテナID> bash
```
