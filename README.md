[README.md](https://github.com/user-attachments/files/34234695/README.md)
# 猫型ロボット：前進2歩・後退2歩
# Cat Robot — Two Steps Forward and Backward
猫型ロボットが前に2歩、後ろに2歩動くPythonアニメーションと、ROS 2による前後移動の制御サンプルです。
## Demo
`cat_robot_two_steps.mp4` を参照してください。
## Features
- 猫型ロボットの歩行アニメーション
- 前進2歩・後退2歩の動作
- Pythonによる動画生成
- ROS 2 Humbleの`/cmd_vel`を使った速度指令サンプル
## Environment
ROS 2制御コードの想定環境：

- Ubuntu 22.04
- ROS 2 Humble
- Gazebo Fortress
- Python 3

## Usage
動画生成：

```bash
python3 make_video.py
```

ROS 2の移動指令：

```bash
source /opt/ros/humble/setup.bash
python3 cat_two_steps.py
```

ROS 2側の実行には、対応するロボットモデルと`/cmd_vel`の受信先が必要です。

## Notes

この動画はPythonで作成したアニメーションです。実機やGazeboの動作を録画したものではありません。

ROS 2コードは差動二輪ロボット向けの前後移動指令の例であり、四足ロボットの関節歩行を直接制御するものではありません。
## YouTube用動画（macOS/Ubuntu共通）
https://youtu.be/G7cwaA_8Kes?si=AdlZ-IYocM_-Z5fa

`cat_robot_two_steps.mp4` は1080pではなく960×540、24fps、8秒、音声なしのデモ動画です。猫の足の動きはPython/Pillowで描いたアニメーションです。Gazeboの録画ではありません。

再生成：
```bash
python3 -m pip install Pillow
sudo apt install ffmpeg  # Ubuntuの場合。Macなら brew install ffmpeg
python3 make_video.py
```

## Ubuntu 22.04 / ROS 2 Humble / Gazebo Fortress
元記事のDiffDriveプラグインを搭載したロボットをGazeboで起動し、ROS 2とGazeboをブリッジした状態で、別ターミナルから実行：
```bash
source /opt/ros/humble/setup.bash
ros2 run ros_ign_bridge parameter_bridge '/cmd_vel@geometry_msgs/msg/Twist]ignition.msgs.Twist'
```
別ターミナル：
```bash
source /opt/ros/humble/setup.bash
python3 cat_two_steps.py
```
`cat_two_steps.py` は速度指令を前後各2回・1秒間送るデモです。**足関節の歩行制御ではありません**。Gazebo側が差動二輪なら車輪で移動します。「歩数」は時間区間として定義した演出上の数え方です。動画の猫の足運びとは同期していません。

## 元記事との差異
記事は差動二輪ロボット、SDF、DiffDrive、`/cmd_vel`、ROS-Ignitionブリッジを使用。ここでは同じ `/cmd_vel` インターフェースを採用していますが、猫の四足歩行は映像演出です。
