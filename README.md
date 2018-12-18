# udacity-p2-continuous-control
Deep Reinforcement Learning Agent: A robot arm learns to reach a position.

## Getting Started

### Preparation

You need to install the required python packages to be able to run this project. The required python packages are listed in `environment.yml`, which is a [conda](https://conda.io/docs/index.html) environment file. It will create a conda environment named `drlnd`.


```bash
conda env create -f conda-environment.yml
conda activate drlnd
```

Next, you need to download one of the binaries that actually provide the environment that you will run you agent in. Choose the one that matches your operating system.

- Linux: [click here][reacher-linux]
- Linux (headless): [click here][reacher-linux-headless]
- Mac OSX: [click here][reacher-osx]
- Windows (64-bit): [click here][reacher-windows]

Once you downloaded the file, unzip it at the root of this project. For example, if you run this project in Linux without access to the display,

```bash
$ cd /path/to/udacity-drlnd-p2-continuous-control
$ curl -LO https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Linux_NoVis.zip
$ unzip Reacher_Linux_NoVis.zip
$ ls -l Reacher_Linux_NoVis
total 59324
drwxr-xr-x 6 handol handol     4096 Jul  4 02:39 Reacher_Data
-rwxr-xr-x 1 handol handol 30358716 Jan 29  2018 Reacher.x86
-rwxr-xr-x 1 handol handol 30382872 Jan 29  2018 Reacher.x86_64
```

Now, you're ready to train the agent.

[reacher-linux]: https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Linux.zip
[reacher-linux-headless]: https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Linux_NoVis.zip
[reacher-osx]: https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher.app.zip
[reacher-windows]: https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Windows_x86_64.zip

## Training The Agent

You can see how to train the agent in Jupyter notebook `Report.ipnb`. To run the notebook, first start up Jupyter server with the following command.

```bash
(base)$ conda activate drlnd
(drlnd)$ jupyter notebook
[I 07:12:35.811 NotebookApp] Serving notebooks from local directory: /path/to/udacity-drlnd-p2-continuous-control
...
    Copy/paste this URL into your browser when you connect for the first time,
    to login with a token:
        http://localhost:8888/?token=e406adf4c029503d5eae4888ec3bc9eb8b7f9a653e9d06bd
```

It will open up the web browser. If not, open the browser manually and go to the URL as noted in the output.

From the file list, open up `Report.ipynb` notebook. If you runs the notebook, the agent successfully achieves the goal within 1000 episodes most of the time.

The successfully trained DQN parameters is saved in the file `p1_dqn_agent.pth`. When the file was recorded the agent reached the goal at episode **330**.


## Learning Algorithm

The agent is trained using [Deep Q-Learning algorithm][dqn-paper] along with the following hyperparameters.

* Neural network for action-value estimation function

  - Network architecture
    - Input: 37 dimension vector
    - Hidden Layer 1
      - Linear with 256 nodes
      - Relu
    - Hidden Layer 2
      - Linear with 128 nodes
      - Relu
    - Output Layer
      - Linear with 4 nodes

  - Optimization algorithm
    - Adam
    
  - Learning rate
    - 5e-4

* Epsilon anealing for e-greedy policy

  - Start: 1.
  - End: 0.01
  - Decay: 0.995
  
* Discount factor, $\gamma$

  - 0.99
  
* Soft-update ratio, $\tau$

  - 0.001

* Network update interval

  - The local and target networks are updated every 4 time steps.
  
* Replay buffer size

  - 10^5
  
* Minibatch size

  - 64
  
With the above hyperparameters, the average score of the last 100 consecutive episodes reached 13.0 after 330 episodes.

[dqn-paper]: https://storage.googleapis.com/deepmind-media/dqn/DQNNaturePaper.pdf

## Ideas for Future WOrk
