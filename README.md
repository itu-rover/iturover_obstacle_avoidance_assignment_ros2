<p align="center">
  <img src="https://github.com/itu-rover/iturover_obstacle_avoidance_assignment/assets/99661459/ac4adfa5-b237-4c0e-9f1e-56532de83b65" alt="iturover" width="300"/>
</p>
<p align="center">
  <em>My battery is low and it's getting dark.</em>
</p>


# ITU Rover Obstacle Avoidance Robot Assignment

Bu ödevde göreviniz Turtlebot simülasyonu kullanarak reaktif şekilde engelden kaçınma algoritması geliştirmek olacaktır. Robot önüne çıkan engellerden _/scan_ topic'inden gelen [LaserScan](https://docs.ros2.org/humble/api/sensor_msgs/msg/LaserScan.html) mesaj türündeki veriyi kullanarak kaçınmalıdır. Robot etrafındaki engelleri tespit etmek için lazer tarayıcı kullanmalı ve aşağıdaki şekilde hareket etmelidir.

<br>
<br>




* Hızını önündeki engel durumuna göre değiştirmeli.
* Önündeki engellere göre uzaktan manevra yapmalı.
* Robotun hareketi boyunca hızının aynı olması ve robot süpürgeler gibi durduğu yerde dönmesi istenmemektedir.
* Smooth bir hareket gözlenmelidir.


<br>
<br>




<p align="center">
  <img src="https://github.com/itu-rover/iturover_obstacle_avoidance_assignment/assets/99661459/e3828def-fe18-4531-a2a4-796c0e6797b1" alt="harita" width="1200"/>
</p>
<p align="center">
  <em>Robotun hareketini gerçekleştireceği parkur</em>
</p>
<br>
<br>




Robotun hareket süresi 60 saniyedir. Bu süre boyunca koridorda başlangıç noktasından olabildiğince uzaklaşmalıdır. 60 saniyenin sonrasında simülasyon ortamının ışığı söndürülmeli ve robot hareketini sonlandırmalıdır. Robotun hareketi aşağıdaki örnekteki gibi olmalıdır.

<br>
<br>






https://github.com/itu-rover/iturover_obstacle_avoidance_assignment/assets/99661459/6ad153ed-4203-452b-babd-e2b1d091dcd2






<br>
<br>



Ödevle ilgili daha fazla bilgiye ve yardımcı olacak kaynaklara aşağıdan ulaşabilirsiniz.

# Kurulum

Bir workspace oluşturun ve bu paketi klonlayıp derleyin.

```bash
mkdir -p ~/rover_ws/src
cd ~/rover_ws/src
git clone https://github.com/itu-rover/iturover_obstacle_avoidance_assignment
cd ~/rover_ws
colcon build
source install/setup.bash
```

İçerisinde launch dosyası olan yeni bir ROS 2 paketi oluşturun:

```bash
cd ~/rover_ws/src
ros2 pkg create --build-type ament_python reactive_robot --dependencies std_msgs rclpy geometry_msgs sensor_msgs gazebo_msgs
mkdir -p reactive_robot/launch
```


# Kullanım

Turtlebot simülasyonunu kullanmak için gerekli paketleri kurun:

```bash
sudo apt install ros-humble-turtlebot3 ros-humble-turtlebot3-simulations ros-humble-gazebo-ros-pkgs
```

Gazebo ve RViz2'yi çalıştırmak için aşağıdaki komutu terminal yardımıyla çalıştırın:

```bash
ros2 launch reactive_robot_sim reactive_robot_sim.launch.py
```


## İsterler ve Kısıtlamalar
<br>
<br>




* Robot bir komut ile harekete geçmelidir.
* Robot harekete geçtikten sonra 60 saniye hareket etmelidir.
* Robot, hareketi esnasında **lazer tarayıcıdan gelen veriyi kullanarak** herhangi bir engele çarpmadan hareket etmelidir.
* 60 saniyelik sürenin sonunda robot hareketini sonlandırmalı, _/scan_ topic'inden unsubscribe olmalı (`destroy_subscription`) ve node kapanmalıdır.
* 60 saniyelik sürenin sonunda Gazebo ortamındaki _sun_ adlı ışık Gazebo service'i olan _/delete_entity_ (`gazebo_msgs/srv/DeleteEntity`) yardımıyla kaldırılmalıdır.
* Robotun hareketindeki değişimler `self.get_logger().info(...)` yardımıyla terminalde gösterilmelidir. Örneğin: _Started rotating left._ Her değişim için yapmayı unutmayınız.
* Node ile ilgili bilgiler `self.get_logger().info(...)` yardımıyla terminalde gösterilmelidir. Örneğin: _Time limit reached. Stopping..._
* Script'iniz ve simülasyon ortamı aynı anda launch dosyası yardımıyla çalıştırılmalıdır.
* Launch dosyasının ismi `reactive_robot.launch.py` olmalıdır.
* Robotun hareketini ayarlamak için kullanacağınız değişkenlerin değerleri (parametreler) oluşturacağınız launch dosyasından çekilmelidir.
* Kodunuz yorum satırlarıyla açıklanmalıdır.

<br>
<br>




# Ayrıca bakınız

* https://docs.ros.org/en/humble/Tutorials.html
* https://docs.ros2.org/humble/api/geometry_msgs/msg/Twist.html
