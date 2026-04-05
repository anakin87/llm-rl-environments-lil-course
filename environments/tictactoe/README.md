# tictactoe

### Overview

**For a detailed walkthrough of this environment and how to use it for training and evaluation, check out the [LLM RL Environments Lil Course](https://github.com/anakin87/llm-rl-environments-lil-course)**

- **Environment ID**: `tictactoe`
- **Short description**: Multi-turn Tic-Tac-Toe. The LLM plays as X against an opponent with configurable probability of moving randomly.
- **Tags**: games, train, eval, tictactoe

### Datasets
- **Primary dataset(s)**: Procedurally generated game episodes

### Task
- **Type**: multi-turn
- **Parser**: XMLParser
- **Rubric overview**: Win/draw/loss reward, format compliance, invalid move penalty

### Quickstart
Run an evaluation with default settings:

```bash
prime eval run tictactoe
```

Configure model and sampling:

```bash
prime eval run tictactoe   -m gpt-4.1-mini   -n 20 -r 3 -t 1024 -T 0.7   -a '{"min_random_move_prob": 0.0, "max_random_move_prob": 0.2}'
```

Notes:
- Use `-a` / `--env-args` to pass environment-specific configuration as a JSON object.

### Environment Arguments

| Arg | Type | Default | Description |
| --- | ---- | ------- | ----------- |
| `num_examples` | int | `1000` | Number of game episodes to generate |
| `min_random_move_prob` | float | `0.0` | Minimum probability opponent moves randomly (vs optimal minimax) |
| `max_random_move_prob` | float | `1.0` | Maximum probability opponent moves randomly (vs optimal minimax) |
| `max_turns` | int | `8` | Maximum number of turns before forced termination |
| `num_groups` | int | `1` | Number of stratified difficulty buckets. For stable training, set this equal to the number of unique prompts per batch (`batch_size // group_size`). |

### Metrics

| Metric | Meaning |
| ------ | ------- |
| `win_reward_func` | 1.0 for win, 0.5 for draw, 0.0 for loss/timeout |
| `format_reward_func` | Parser-driven format compliance (weight: 0.2) |
| `invalid_move_penalty_func` | -0.1 flat penalty if any invalid move occurred |
