# pytorch-a2c-ppo-acktr

A PyTorch implementation of PPO for use with the pretrained models provided in [Assistive Gym](https://github.com/Healthcare-Robotics/assistive-gym).  
This library includes scripts for training and evluating multi agent policies using co-optimization; specifically, [train_coop.py](https://github.com/Zackory/pytorch-a2c-ppo-acktr/blob/master/ppo/train_coop.py) and [enjoy_coop.py](https://github.com/Zackory/pytorch-a2c-ppo-acktr/blob/master/ppo/enjoy_coop.py).

## Installation and pretrained models
This library and the pretrained policies for Assistive Gym can be downloaded using the following commands.  
If you do not have `wget` installed on your machine, you can download the models directly from the [Assistive Gym GitHub release page](https://github.com/Healthcare-Robotics/assistive-gym/releases/download/0.100/pretrained_policies.zip).
```bash
# Install PyTorch RL library
pip3 install git+https://github.com/Zackory/pytorch-a2c-ppo-acktr --no-cache-dir
# Install OpenAI Baselines
pip3 install git+https://github.com/openai/baselines.git
# Download pretrained policies
cd assistive-gym
wget -O trained_models/ppo/pretrained_policies.zip https://github.com/Healthcare-Robotics/assistive-gym/releases/download/0.100/pretrained_policies.zip
unzip trained_models/ppo/pretrained_policies.zip -d trained_models/ppo
```
If you receive an error during installation due to MPI (mpi4py), you may need to install the missing MPI package. On Linux, this can be resolved with:
```bash
sudo apt install libopenmpi-dev
```
or on Mac with:
```bash
brew install mpich
```

## Examples
Refer to [Assistive Gym](https://github.com/Healthcare-Robotics/assistive-gym) for more detailed use cases of this reinforcement learning library.

### Training - Static human
```bash
python3 -m ppo.train --env-name "ScratchItchJaco-v1" --num-env-steps 10000000
```
We suggest using `nohup` to train policies in the background, disconnected from the terminal instance.
```bash
nohup python3 -m ppo.train --env-name "ScratchItchJaco-v1" --num-env-steps 10000000 --save-dir ./trained_models/ > nohup.out &
```
See [arguments.py](https://github.com/Zackory/pytorch-a2c-ppo-acktr/blob/master/ppo/a2c_ppo_acktr/arguments.py) for a full list of available arguments and hyperparameters.

### Training - Co-optimization, active human and robot
```bash
python3 -m ppo.train_coop --env-name "FeedingSawyerHuman-v1" --num-env-steps 10000000
```
### Resume training from an existing policy
```bash
python3 -m ppo.train --env-name "FeedingSawyer-v1" --num-env-steps 2000000 --save-dir ./trained_models_new/ --load-policy ./trained_models/ppo/FeedingSawyer-v1.pt
```
### Visual Evaluation - Static human
```bash
python3 -m ppo.enjoy --env-name "ScratchItchJaco-v1"
```
### Visual Evaluation - Co-optimization, active human and robot
```bash
python3 -m ppo.enjoy_coop --env-name "FeedingSawyerHuman-v1"
```
### Quantitative Evaluation over 100 trails - Static human
```bash
python3 -m ppo.enjoy_100trials --env-name "ScratchItchJaco-v1"
```
### Quantitative Evaluation over 100 trails - Active human from co-optimization
```bash
python3 -m ppo.enjoy_coop_100trials --env-name "FeedingSawyerHuman-v1"
```

## pytorch-a2c-ppo-acktr-gail
This library is derived from code by Ilya Kostrikov: https://github.com/ikostrikov/pytorch-a2c-ppo-acktr-gail

Please use this bibtex if you want to cite this repository in your publications:

    @misc{pytorchrl,
      author = {Kostrikov, Ilya},
      title = {PyTorch Implementations of Reinforcement Learning Algorithms},
      year = {2018},
      publisher = {GitHub},
      journal = {GitHub repository},
      howpublished = {\url{https://github.com/ikostrikov/pytorch-a2c-ppo-acktr-gail}},
    }

## Requirements

* Python 3
* [PyTorch](http://pytorch.org/)
* [OpenAI baselines](https://github.com/openai/baselines)
