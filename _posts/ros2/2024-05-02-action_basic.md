---
layout: single
title: "[ROS2] Action 기초"

categories:
  - ros2

date: 2024-05-02
last_modified_at: 2024-05-02

---
<br>
ROS2 Action 기초
<br>

# 0. Action 기초

> 이번에는 Service와 Topic이 같이 합쳐진? Action에 대해서 공부를 해본다. Action 또한 통신 방식 중 하나이다.
> 

<br>

---

<br>

# 1.Action 이란?


![https://github.com/gubam/gubam.github.io/assets/109836946/34d2a4b5-3041-400f-b6a8-3848f5242bba](https://github.com/gubam/gubam.github.io/assets/109836946/34d2a4b5-3041-400f-b6a8-3848f5242bba)

액션은 위의 사진을 보면 바로 이해가 가능할 것이다.  2개의 Service와 한 개의 Topic이 Action내부에 존재를 하고 노드에는 Action Client와 Action Server가 존재한다. 그럼 해당 Service와 Topic이 어떤 기능을 할까?

Action 내부의 Service와 Topic의 이름을 보면 대충 유추가 가능하다. 어떠한 목표 값을 Goal Service로 보내고 그 바뀌는 동안의 정보를 Feedback Topic으로 보내주고 목표에 도달했으면 Result Service가 실행이 된다. 

특징은 실행 중인 목표치를 중간에 취소할 수도 있고 변경을 할 수 있다고 한다.

<br>

---

<br>

# 2. Action 명령어

```docker
ros2 action list -t
ros2 action info <action_name>
ros2 interface show <action_type>
```

Action도 이전의 Service와 Topic과 비슷한 명령어를 가지고 있다. 위의 list 확인 명령어로 Action의 종류와 해당 Action들의 타입을 확인 할 수 있고 info 명령어를 이용해서 해당 Action의 Clients와 Server노드를 확인 할 수 있다.

interface show를 이용하면 해당 action의 각 데이터 들을 확인할 수 있다. 이 명령어를 turtlesim에 구현된 action으로 확인을 해보면 아래와 같은 출력이 나온다.(action은 확장자가 .action이라고 한다.)

```docker
# The desired heading in radians
float32 theta
---
# The angular displacement in radians to the starting position
float32 delta
---
# The remaining rotation in radians
float32 remaining
```

가장 위쪽 theta가 goal의 값이고 delta는 result 그리고 remaining은 feedback의 값이다. 이 역시 “-” 3개를 이용해서 구분을 한 것을 확인 가능하다. 이것을 어떻게 확인을 하는지는 아래의 명령어를 사용해보면 확인을 할 수 있다.

```docker
ros2 action send_goal <action_name> <action_type> <values> --feedback
```

위의 명령어는 이름부터 알 수 있을 것 같다. send_goal 즉 목표 값을 action에 넣어주는 것이다.

이것을 한번 turtlesim을 이용하여 실행을 해보았다.

![https://github.com/gubam/gubam.github.io/assets/109836946/901ce902-e137-452d-9898-a93a74262629](https://github.com/gubam/gubam.github.io/assets/109836946/901ce902-e137-452d-9898-a93a74262629)

value값은 “{theta: 0.1}”로 주었고 초기 theta의 값은 0.0으로 설정을 하였다. 위의 사진을 보면 sending goal, Feedback, Result를 확인 할 수 있다.  그리고 각 데이터들은 theta, remaining, delta인것을 보아 위쪽의 interface를 한 것과 동일한 것도 알 수 있다. 

즉 해당 액션은 원하는 각도를 보내고 피드백으로 해당 각도까지 남은 각도를 보내주고 목표 값에 도달하고 초기로부터 각도 변화량을 결과로 보내주는 Action이라고 생각하면 될 것 같다.

<br>

---

<br>

# 3. 결론

기본적인 Topic, Message, Action을 알아보았다. 다들 비슷하면서 특징을 가진 것 같아 보인다. 앞으로는 이러한 것들을 어떻게 만드는지에 대해서 알아가 보겠다. 

출처 : [https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Actions/Understanding-ROS2-Actions.html](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Actions/Understanding-ROS2-Actions.html)
