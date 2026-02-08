# Reinforcement-Learning-for-Fuel-Efficient-Driving
This project implements Q-learning from scratch to solve the OpenAI Gym’s MountainCar-v0 with state (position, velocity) discretization and an epsilon-greedy exploration strategy. Includes a custom reward shaping function, training over 1,000 episodes.
---

## Repository contents

- `Mountain_car.ipynb`  
  Implements Q-learning, reward shaping, training logs, and plots (Average Reward vs Episodes + policy/action visualization).

- `CarEnvironment.py`  
  Implements a custom `gym.Env` called `CarEnvironment` with:
  - Action space: `spaces.Discrete(3)`  
  - Observation space: `(position, velocity)` as a `spaces.Box`  
  - Fuel level that decreases with acceleration  
  - Shaped reward and termination conditions  
  - Rendering using `pygame` via `render_mode`

---

## Method overview

### 1) Q-learning (tabular)

The notebook trains a Q-table with:
- State discretization for the continuous `(position, velocity)` observation space (uses a `[10, 50]`-style discretization).
- Epsilon-greedy action selection. 
- Standard Q-learning update using learning rate and discount factor.

Reward shaping is done with:
- `newreward(pos)` (returns a small positive reward after reaching a position threshold, otherwise a shaped value based on position).

---

## Training & outputs

- Training runs for **1,000 episodes** and prints “Clear on episode …” when the goal condition is met, plus periodic average reward logs.
- Produces plots such as **Average Reward vs Episodes** and action/policy visualizations (initial vs final action distributions).

---

## Custom environment (`CarEnvironment.py`)

`CarEnvironment` is a Gym-compatible environment that extends `gym.Env`.

### Spaces
- `action_space = spaces.Discrete(3)` (three discrete actions).
- `observation_space = spaces.Box(low, high, dtype=np.float32)` where the observation is `[position, velocity]`.

### Key features
- Has position bounds and speed bounds, plus a `goalposition`.
- Tracks `fuellevel` (initial fuel is set and decreases when accelerating).
- Defines custom termination logic and shaped reward logic; includes an additional high reward when reaching the goal with sufficient remaining fuel.

### Rendering
- `render()` uses `pygame` and supports `render_mode="human"` (and an RGB-array style mode).
- If `pygame` is missing, it raises an error indicating the dependency requirement.


## Demo screenshots

![Demo screenshot 1](Demo%20screenshots/4.jpg)
![Demo screenshot 2](Demo%20screenshots/5.jpg)
![Demo screenshot 3](Demo%20screenshots/6.jpg)
![Demo screenshot 4](Demo%20screenshots/7.jpg)
![Demo screenshot 5](Demo%20screenshots/8.jpg)

---

## Setup

### Create a virtual environment (recommended)
```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
# .venv\Scripts\activate    # Windows
```
## How to run

### Option A: Run the notebook (Gym MountainCar-v0)

Open and run:

- `Mountain_car.ipynb`

The notebook creates the environment as:

```python
import gym
env = gym.make("MountainCar-v0")
```
