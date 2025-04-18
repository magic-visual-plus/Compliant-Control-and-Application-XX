## 修改点
1.修改定点导纳的x0为实时位置



## 启动环境
#### 启动 gazebo
```
roslaunch ur_gazebo ur5e_bringup.launch transmission_hw_interface:=hardware_interface/PositionJointInterface specified_controller:=cartesian_position_controller

```

#### 启动导纳
```
roslaunch admittance Admittance.launch INTERFACE_TYPE:=position
```

#### 设置期望力

仿真position控制指令设置
<!-- 发送期望力 -->
```
rostopic pub -1 /wrench_desired geometry_msgs/WrenchStamped "{wrench: {force: {z: 0}}}"
```
<!-- 发送环境接触力 -->
rostopic pub -1 /wrench_fake geometry_msgs/WrenchStamped "{wrench: {force: {z: 0}}}"

<!-- 环境力也可以通过代码来模拟 -->
Admittance.cpp L200处实现 刚度为500的环境力设置