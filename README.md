# OpenAI-Gym

## Installation

|Environment|Name|
|:---------:|:--:|
|OS         |Ubuntu 18.04|
|C++        |17|
|Python     |3.7.3|

1. Basic package

```
sudo -H pip3.6 install gym
```

​	ココらへんは複雑で，基本的には，pipのバージョンは３．７となっているがanacondaやminicondaでバージ	ョン管理していると明示的にバージョンを指定しないといけないことがある．

2. Optional package

```sh
sudo apt install python-numpy python-dev cmake zlib1g-dev libjpeg-dev xvfb xorg-dev python-opengl libboost-all-dev libsdl2-dev swig
```

3. Atari games

```sh
sudo -H pip install 'gym[atari]'
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