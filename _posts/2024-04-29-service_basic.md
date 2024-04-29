---
layout: single
title: "[ROS2] Service 기초"

categories:
  - ros2

date: 2024-04-29
last_modified_at: 2024-04-29

---
<br>
ROS2 Service 기초
<br>
# Service 기초

Created by: 조규범
Last edited: April 29, 2024 9:51 PM

# 0. Service 기초

> ros에서 기본이 되는 단위들이 존재한다. 그 중에서 Service의 기본적인 사용법에 대해서 알아보았다. (책과 사이트 따라서 turtlesim을 이용해서 공부를 하였다.)
> 

---

# 1. Service란?

![[https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Services/Understanding-ROS2-Services.html](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Services/Understanding-ROS2-Services.html)](Service%20%E1%84%80%E1%85%B5%E1%84%8E%E1%85%A9%200e51e7d9f79044059d02d25472fbc8a0/Untitled.png)

[https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Services/Understanding-ROS2-Services.html](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Services/Understanding-ROS2-Services.html)

- Service란 여러개의 노드가 통신을 하는 방법중 한개로 call-and-response model 즉 요청을 하면 그 요청에 대한 응답을 하는 모델이다.  위의 그림을 보면 조금 더 직관적으로 이해를 할 수 있다.
- 왼쪽은 Service Client 즉 요청을 하는 노드이고 우측 위쪽은 Service Server 노드로 요청에 대한 응답을 하는 노드이다. 만약 client 노드가 어떤 서비스를 형식에 맞게 요청을 하면 그에 대한 응답을 해주는 구조이다.
- 단 응답은 꼭 존재하지 않아도 된다. (어떤 것을 실행하던지 저장을 하던지 뭔가를 하겠지?)

---

# 2. 기본 명령어

```bash
ros2 service list
ros2 service type <service_name>
```

- 위의 두 개의 명령어는 기본적인 이름을 알아내는 용도라고 생각을 하면 된다. 위의 명령어를 통해서 현재 활성화 되어있는 node의 service들의 이름을 알 수 있고 해당 이름을 이용하여 아래 명령어를 통해서 서비스의 타입을 알아낼 수 있다.

```bash
ros2 interface show <type_name>
```

- 여기서 서비스의 타입이란 일종의 구조체와 비슷하다. 해당 구조는 위의 명령어로 확인이 가능하다.
- 서비스의 타입은 srv라는 확장자를 가지게 된다. turtlesim의 /spawn이라는 서비스의 타입은 아래와 같이 나온다.

```docker
float32 x
float32 y
float32 theta
string name # Optional.  A unique name will be created and returned if this is empty
---
string name
```

- 위의 ‘---’를 기준으로 위쪽은 요청하는 자료의 구조 그리고 아래는 응답을 하는 자료의 구조이다. 한 마디로 float32의 x, y, theta와 string 의 name을 받게 되면 name을 응답으로 뱉어내는 것이다.

```docker
ros2 service call <service_name> <service_type> <arguments>
```

- 그럼 이렇게 알아낸 서비스를 어떻게 사용하냐! 바로 위의 명령어로 service를 call 해주면 된다.
- name과 type을 적어주고 argument 즉 요청 시 필요한 정보들을 입력해 주면 서비스가 요청이 된다.

```docker
ros2 service call /spawn turtlesim/srv/Spawn "{x: 2, y: 2, theta: 0.2, name: 'gubam'}"
```

- turtlesim의 /spawn 서비스를 기준으로 위와 같이 요청을 한다. 여기서 arguments를 적을 때 띄어쓰기를 유의해서 적어주어야 한다.
- 위와 같은 요청을 하면 turtlesim에 거북이 한 마리가 설정한 위치에 더 생기고 해당 namespace(gubam)에 대한 서비스도 추가적으로 생기게 될 것이다.

---

# 3. 마무리

> service의 간단한 사용법과 구조를 살펴보았다. 아직 시작이라서 틀린 정보가 많을 수 있으니 공부를 하면서 조금씩 채워가겠다.
>
