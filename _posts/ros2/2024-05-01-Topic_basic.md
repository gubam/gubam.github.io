---
layout: single
title: "[ROS2] Topic 기초"

categories:
  - ros2

date: 2024-05-01
last_modified_at: 2024-05-01

---
<br>
ROS2 Topic 기초
<br>

# 0.  Topic 기초

> 앞선 글에서 Service에 대해서 글을 썼다. 마찬가지로 노드 사이를 연결할 수 있는 토픽에 대해서 알아보겠다.
> 

---

# 1. Topic이란?

![topic 사진](https://github.com/gubam/gubam.github.io/assets/109836946/4981ff00-701f-467e-a39f-10a9e4f7d47b)

<br>

- Topic이란 Service와 마찬가지로 노드 사이의 통신을 하는 방식 중 하나이다. 다만 Service와 차이를 살펴보면 Service는 노드가 request(요청)을 하면 다른 노드에서 response(응답)을 해주는 일종의 양방향 통신을 하고 그 응답은 요청한 노드만 받는 방식이었다.
- Topic은 Service와 다르게 Publisher가 Message를 보내면 해당 Topic을 구독하고 있는 Subscriber들이 해당 Message를 받는 방식이다.
- 그리고 그림에서 볼 수 있듯이 특정 Topic에 대한 Publisher와 Subscriber 노드는 여러 개가 존재할 수 있다는 점에서도 이전의 Service와 차이를 지니고 있다.

<br>

---

<br>

# 2. 기본 명령어

```bash
ros2 topic list
ros2 service type <service_name>
```

- 기본적으로 명령어는 Service와 비슷하다. topic의 리스트들의 이름을 보고 해당 topic의 type을 확인할 수 있다.

<br>

```bash
ros2 topic list -t
```

- 위의 명령어를 사용하게 되면 type도 한번에 출력을 할 수 있다.
- 
<br>

```docker
ros2 topic echo <topic_name>
```

- 위의 명령어를 보자 리눅스에서 echo는 일종의 print? 같은 역할을 한다. 그럼 위의 명령어는 어떤 작동을 할까 생각해보면 topic을 출력할 것 같다는 생각이 든다.
- 한번 써보면 해당 topic의 message가 계속 출력이 되는 것을 확인 할 수 있다.
- 즉 echo로 간단한 subscriber 노드를 만든 것이라고 생각할 수 있다.(확인용으로 사용하면 좋을듯)

<br>

```docker
ros2 topic info <topic_name>
```

- 위의 명령어는 topic의 정보를 확인하는 명령어로 type과 publisher와 subscriber의 수를 확인 할 수 있다.
- 
<br>

```docker
ros2 interface show <topic_type>
```

- 이번 명령어는 topic의 msg 구성을 확인 할 수 있는 명령어다. 입력을 하면 msg가 어떻게 구성되어 있는지를 확인해 볼 수 있다.

<br>

```docker
ros2 topic pub <topic_name> <msg_type> '<args>'
ros2 topic pub --rate 1 <topic_name> <msg_type> '<args>'
```

- 앞서 subscriber를 생성(echo 이용) 해봤으면 이번에는 publisher를 간단하게 생성하는 명령이다.  간당하게 위의 interface를 통해서 알게 된  argument의 형식대로 topic에 넣어주면 완료이다!
- 해당 명령어에서 pub의 속도를 조절할 수 있다. 바로 rate 1을 넣어주는 것이다. rate 1은 진동수라고 이해하면 편하다. 즉 1초에 1번 pub을 진행한다는 것이고 2를 넣으면 1초에 2번 pub을 한다는 것이다.

<br>

```docker
ros2 topic hz <topic_name>
```

- 만약 topic에서 msg전달 속도를 알고 싶다면 위의 명령어를 사용한다. 해당 명령어 사용 시에 사용한 시점을 기준으로 속도를 측정하게 된다.
  
<br>

---

<br>

# 3. 마무리

> 이번에는 topic에 대해서 알아 봤다. 사실 현재는 서비스보다는 이 topic을 많이 사용할 것 같다는 생각이 든다. 원래는 action도 같이 작성하려고 했는데 생각보다 오래 걸려서 따로 작성을 하겠다.

출처 : <https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Services/Understanding-ROS2-Services.html>
