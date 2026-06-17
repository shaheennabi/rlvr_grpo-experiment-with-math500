# RLVR-GRPO Experiment with Math500

This repository contains a small experiment evaluating a base model against RLVR-GRPO checkpoints on the Math500 evaluation set.

## Evaluation Results

### Base Model

- Correct: **32 / 50**
- Accuracy: **64.0%**
- Total evaluation time: **7.8 minutes**
- Average response length: **303.0 tokens**

### RLVR-GRPO (5-Step Checkpoint)

Training configuration:

- GRPO steps: **5**
- Rollouts: **4**
- Max generation length: **300 tokens**
- Sparse binary reward (correct answer = 1, incorrect answer = 0)

Evaluation results:

- Correct: **24 / 50**
- Accuracy: **48.0%**
- Total evaluation time: **5.9 minutes**
- Average response length: **223.4 tokens**

### RLVR-GRPO (50-Step Checkpoint)

Training configuration:

- GRPO steps: **50**
- Rollouts: **8**
- Max generation length: **300 tokens**
- Sparse binary reward (correct answer = 1, incorrect answer = 0)

Evaluation results:

- Correct: **30 / 50**
- Accuracy: **60.0%**
- Total evaluation time: **3.9 minutes**
- Average response length: **219.2 tokens**

---

## Initial Observations

- The 5-step RLVR-GRPO checkpoint underperformed the base model, dropping from **64% → 48%** accuracy.
- The 50-step RLVR-GRPO checkpoint recovered much of the lost performance, improving from **48% → 60%** accuracy.
- The final RLVR-GRPO checkpoint remained slightly below the base model (**60% vs 64%**), although the difference corresponds to only **2 questions** on a 50-problem evaluation set.
- Response lengths decreased substantially after RL training (**303 → ~220 tokens**), suggesting the policy learned shorter solution trajectories.
- Evaluation latency also decreased as response lengths became shorter.
- Training used a sparse reward signal based only on final answer correctness, providing limited learning signal compared to denser reward formulations.
- These results suggest that the GRPO implementation is functioning correctly and that learning occurred during training. However, additional training steps, larger evaluation sets, and improved reward design are likely needed to determine whether RLVR-GRPO can consistently outperform the base model.

## What is RLVR-GRPO?

RLVR-GRPO is a reinforcement learning variant of GRPO that optimizes a model policy using rollout-based policy updates and a sparse binary reward defined by final answer correctness. In this experiment, RLVR-GRPO seeks to learn shorter, more accurate reasoning trajectories on Math500 problems while trading off generation length and evaluation speed.

## Full Codebase Support

For the complete implementation and full codebase support, see: https://github.com/shaheennabi/open-posttraining-system/tree/main

