# Connect 4 Neural Network

A Connect 4 game AI trained using Deep Q-Learning (DQN) with PyTorch. The agent has been trained through 176,000 episodes of self-play to learn optimal Connect 4 strategies.

## Overview

This project implements a reinforcement learning agent that learns to play Connect 4 through deep Q-learning. The AI uses a neural network to evaluate board positions and select moves, improving its strategy through self-play and experience replay.

## Features

- Deep Q-Network (DQN) implementation with PyTorch
- Experience replay buffer for stable training
- Epsilon-greedy exploration strategy
- Target network for improved convergence
- GPU acceleration support (CUDA)
- Play against the trained AI interactively
- Saved model checkpoints at regular intervals

## Project Structure

```
backend/
├── main.py              # Main training script
├── training.py          # Training loop and logic
├── model.py             # QNetwork neural network architecture
├── environment.py       # Connect 4 game environment
├── replay_buffer.py     # Experience replay buffer
├── play_against_ai.py   # Interactive game against AI
├── models/              # Saved model checkpoints
└── Notes.md            # Training process documentation
```

## Requirements

- Python 3.12+
- PyTorch
- NumPy

## Installation

1. Clone the repository:

```bash
git clone <repository-url>
cd connect-4-neural-net
```

2. Create a virtual environment:

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:

```bash
pip install torch numpy
```

## Usage

### Play Against the AI

Run the interactive game script to play against the trained model:

```bash
cd backend
python play_against_ai.py
```

You play as Player 1, and the AI plays as Player 2. Choose your column (0-6) when prompted.

### Train the Model

To train the model from scratch or continue training:

```bash
cd backend
python main.py
```

Model checkpoints are automatically saved in `backend/models/` every 1,000 episodes.

## How It Works

The agent uses Deep Q-Learning with the following components:

1. **Q-Network**: Neural network that estimates Q-values for each action (column choice)
2. **Experience Replay**: Stores past game states to break correlation between consecutive samples
3. **Target Network**: Separate network for stable Q-value targets during training
4. **Epsilon-Greedy Policy**: Balances exploration (random moves) and exploitation (learned strategy)

### Training Process

1. Agent plays Connect 4 games against itself
2. Experiences (state, action, reward, next_state) are stored in replay buffer
3. Neural network trains on random batches from the buffer
4. Exploration rate (epsilon) gradually decreases as learning progresses
5. Target network periodically syncs with main network for stability

For detailed explanation of the training loop, see `backend/Notes.md`.

## Model Performance

The latest model (`connect4_model_176000.pth`) has been trained through 176,000 episodes of self-play, demonstrating strong strategic play including:

- Recognizing winning opportunities
- Blocking opponent threats
- Building tactical positions

## Technical Details

- **Input**: 6x7 board representation (42 values: 1 for player pieces, -1 for opponent, 0 for empty)
- **Output**: Q-values for 7 possible actions (one per column)
- **Reward Structure**: Win (+1), Loss (-1), Draw (0), Illegal Move (penalty)
- **Discount Factor (γ)**: Typically 0.99
- **Learning Rate**: Adam optimizer with configurable rate

## Future Enhancements

- Web-based frontend for interactive play
- Multiplayer support
- Different difficulty levels
- Move visualization and board evaluation display
- Tournament mode against different model checkpoints

## License

This project is available for educational and personal use.

## Acknowledgments

Built using reinforcement learning principles and PyTorch deep learning framework.
