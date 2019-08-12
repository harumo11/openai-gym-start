# OpenAI-Gym

## Installation

|Environment|Name|
|:---------:|:--:|
|OS         |Ubuntu 18.04|
|C++        |17|
|Python     |3.7.3|

1. Basic package

```
sudo -H pip3 install gym

or 

pip3 install wheel
pip3 install gym
```

​	ココらへんは複雑で，基本的には，pipのバージョンは３．７となっているがanacondaやminicondaでバージ	ョン管理していると明示的にバージョンを指定しないといけないことがある．

2. Optional package

```sh
sudo apt install python-numpy python-dev cmake zlib1g-dev libjpeg-dev xvfb xorg-dev python-opengl libboost-all-dev libsdl2-dev swig
```

3. Atari games

```sh
sudo -H pip3.6 install 'gym[atari]'
```

4. Checking

   ```python
   import gym
   env = gym.make("CartPole-v1")
   observation = env.reset()
   for _ in range(1000):
     env.render()
     action = env.action_space.sample() # your agent here (this takes random actions)
     observation, reward, done, info = env.step(action)
   
     if done:
       observation = env.reset()
   env.close()
   ```

     ```sh
   python3.6 cart-pole.py
     ```

   

## Links

[OpenAI Gym]([https://gym.openai.com](https://gym.openai.com/))

本家本元のサイト

[OpenAI Github](https://github.com/openai/gym)

OpenAI Gymのgithub

[Classic control](https://gym.openai.com/envs/#classic_control)

利用可能な環境リスト(クラシック限定)

[OpenAI Gym 入門](https://qiita.com/ishizakiiii/items/75bc2176a1e0b65bdd16)

Qiitaの入門記事



## Basic Usage

## Environment

makeの引数に環境名（ゲーム名）を指定し，環境インスタンス`env`を生成

```python
import gym
env = gym.make('MountainCar-v0')
```

生成できる環境の一覧は以下で取得できる

```python
from gym import envs
envids = [spec.id for spec in envs.registry.all()]
```

環境を初期化する

```python
observation = env.reset()
```

`reset()`にて，初期状態の観測データobservationが取得できる

現在の環境を描画

```
env.render()
```

## Observation

MountainCar-v0(山登り)の場合，以下のような配列が観測データとして取得できる．

それぞれの意味は[GitHub wiki MountainCar v0](https://github.com/openai/gym/wiki/MountainCar-v0#observation)

```python
print(observation)
>> [-0.5693232 0. ]
```

|      | 内容     | Min   | Max  |
| ---- | -------- | ----- | ---- |
| 0    | 車の位置 | -1.2  | 0.6  |
| 1    | 車の速度 | -0.07 | 0.07 |

観測データの最小値と最大値は以下で取得

```python
# 観測データの最大値
print(env.observation_space.high)
>> [0.6 0.07]

# 観測データの最小値
print(env.observation_space.low)
>> [-1.2 -0.07]
```

観測データの配列次元は以下で調べられる

```python
print(env.ovservation_space)
>> Box(2,)
```



## Action

環境インスタンス`env`の`step()`関数の非キスにアクションデータを設定する．

MoutainCar-v0(山登り)の場合，アクションの値はそれぞれ以下の通り

| 値   | 内容       |
| ---- | ---------- |
| 0    | 左へ押す   |
| 1    | 何もしない |
| 2    | 右へ押す   |

詳細は[GitHub wiki MountainCar-v0](https://github.com/openai/gym/wiki/MountainCar-v0#actions)に記載されている

```python
# 左
action = 0
observation, reward, done, info = env.step(action)
```

行動を実行した戻り地として，行動後の観測データ・報酬・ゲーム終了フラグ・詳細情報が得られる．

山登りの場合，詳細情報はなく，報酬は各ステップごとに-1と固定



環境ごとの行動の値は以下で調べられる

```python
print(env.action_space)
>> Discrete(3)
```

`Discrete(3)`は３つの離散値`[0,1,2]`



## Summary

1. 環境を生成 `gym.make(環境名)`
2. 環境をリセットして観測データ（状態）を取得 `env.reset()`
3. 状態から行動を決定　←アルゴリズム考えるところ
4. 行動を実行して，行動後の観測データ（状態）と報酬を取得 `env.step(行動)`
5. 今の行動を報酬から評価する　←アルゴリズム考えるところ
6. 3〜５を繰り返す



# gym-http-api

## Installation

1. Package

```sh
git clone https://github.com/openai/gym-http-api
cd gym-http-api
sudo -H pip3 install -r requirements.txt 
```

もし，途中で下記のようなエラーを吐いたら

```sh
    numpy/core/src/multiarray/numpyos.c:18:10: fatal error: xlocale.h: No such file or directory
     #include <xlocale.h>
              ^~~~~~~~~~~
    compilation terminated.
    numpy/core/src/multiarray/numpyos.c:18:10: fatal error: xlocale.h: No such file or directory
     #include <xlocale.h>
              ^~~~~~~~~~~
    compilation terminated.

```

[このページ](https://stackoverflow.com/questions/51041109/numpy-1-11-doesnt-install-in-virtualenv-ubuntu-studio)を見ましょう．

2. Check

   ```sh
   cd opt/gym-http-api
   ```

   2.1 Server

   ```sh
   python3.6 gym_http_server.py
   ```

   特に画面が現れることはないが環境サーバが立ち上がる

   2.2 Client

   ```sh
   python3.6 example_agent.py
   ```



## C++ client

### Installation



