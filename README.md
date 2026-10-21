# Reinforcement Learning

## Temporal differences and action values

- **[Temporal-difference learning](https://link.springer.com/article/10.1007/BF00115009)** — 1988. Learns predictions from differences between successive predictions, rather than waiting only for final outcomes. Establishes convergence and optimality results for specified cases.
- **[Q-learning](https://link.springer.com/article/10.1007/BF00992698)** — 1992. Incrementally estimates action values from experience. Proves convergence under the paper's tabular representation, sampling, and convergence assumptions; this is not a deep-network convergence guarantee.
- **[DQN](https://arxiv.org/abs/1312.5602)** — 2013. Combines convolutional visual representations with Q-learning to estimate future reward from game pixels. The original preprint studies seven Atari games; later DQN evaluations use different protocols and game sets.
- **[Double DQN](https://arxiv.org/abs/1509.06461)** — 2015. Separates action selection from action evaluation in the Q-learning target. Reduces overestimation arising from using the same estimates to select and evaluate an action.
- **[Dueling networks](https://arxiv.org/abs/1511.06581)** — 2015. Splits the action-value network into state-value and action-advantage estimators. Shares learning across actions without requiring a different underlying reinforcement-learning algorithm.
- **[Prioritized experience replay](https://arxiv.org/abs/1511.05952)** — 2015. Samples selected stored transitions more often instead of replaying all experience uniformly. Changes which past interactions drive learning, rather than how the agent collects new data.
- **[Rainbow](https://arxiv.org/abs/1710.02298)** — 2017. Combines six DQN extensions and measures their contributions through ablations. Demonstrates that improvements need to be tested jointly; isolated gains need not simply add together.

## Return distributions

- **[Distributional reinforcement learning](https://arxiv.org/abs/1707.06887)** — 2017. Models the distribution of random returns instead of only their expectation. Develops distributional Bellman analysis and a practical approximate-distribution algorithm, while identifying instability in the control setting.
- **[Quantile regression DQN](https://arxiv.org/abs/1710.10044)** — 2017. Represents the return distribution through quantiles and learns them with quantile regression. Connects approximate distribution learning to a distributional Bellman formulation.

## Policy gradients and actor–critic methods

- **[REINFORCE](https://link.springer.com/article/10.1007/BF00992696)** — 1992. Derives stochastic-network updates aligned with the gradient of expected reinforcement. Covers immediate rewards and specified delayed-reward settings, and connects the updates with backpropagation.
- **[TRPO](https://arxiv.org/abs/1502.05477)** — 2015. Optimizes a policy surrogate with a constraint on policy divergence. The practical algorithm approximates a theoretically justified update; monotonic improvement is not an unconditional implementation guarantee.
- **[Generalized advantage estimation](https://arxiv.org/abs/1506.02438)** — 2015. Uses an exponentially weighted advantage estimator to reduce policy-gradient variance at the cost of bias. Connects advantage estimation to temporal-difference learning with eligibility traces.
- **[A3C](https://arxiv.org/abs/1602.01783)** — 2016. Runs parallel actor-learners with asynchronous parameter updates. Studies how diverse concurrent experience stabilizes deep value and actor–critic learning.
- **[PPO](https://arxiv.org/abs/1707.06347)** — 2017. Alternates interaction with minibatch optimization of a policy surrogate. Its clipped-ratio variant limits incentives for large updates; clipping is not a hard bound on policy divergence.
- **[DDPG](https://arxiv.org/abs/1509.02971)** — 2015. Uses a deterministic policy gradient within an actor–critic architecture for continuous actions. Extends deep Q-learning ideas to settings where enumerating all actions is impractical.
- **[TD3](https://arxiv.org/abs/1802.09477)** — 2018. Uses the minimum of two critic estimates and delays policy updates to reduce effects of approximation error. Addresses overestimated values in continuous-action actor–critic learning.
- **[Soft Actor-Critic](https://arxiv.org/abs/1801.01290)** — 2018. Optimizes reward together with policy entropy using an off-policy stochastic actor–critic. The entropy term encourages varied actions while the critic estimates task value.
- **[SAC temperature adaptation](https://arxiv.org/abs/1812.05905)** — 2018. Extends Soft Actor-Critic with a constrained formulation that tunes the entropy temperature automatically. Studies sensitivity to settings and applications in simulated and physical control.
- **[Control as inference](https://arxiv.org/abs/1805.00909)** — 2018. Connects maximum-entropy control with probabilistic inference. Distinguishes exact inference under deterministic dynamics from a variational treatment under stochastic dynamics.

## Exploration and goal relabeling

- **[Density-based pseudo-counts](https://arxiv.org/abs/1606.01868)** — 2016. Derives visitation-like counts from density models to extend count-based exploration beyond tabular states. Converts estimated novelty into intrinsic rewards.
- **[Intrinsic curiosity module](https://arxiv.org/abs/1705.05363)** — 2017. Uses prediction error in an inverse-dynamics-trained feature space as an intrinsic reward. Encourages exploration through failures to predict action consequences rather than raw pixel reconstruction alone.
- **[Random network distillation](https://arxiv.org/abs/1810.12894)** — 2018. Rewards prediction error against features from a fixed random network. Introduces a novelty signal and a mechanism for combining intrinsic and task rewards.
- **[NoisyNet](https://arxiv.org/abs/1706.10295)** — 2017. Adds parameterized noise to network weights and learns its parameters with the task objective. Produces exploratory policy variation through the network rather than only random action replacement.
- **[Hindsight experience replay](https://arxiv.org/abs/1707.01495)** — 2017. Reuses unsuccessful goal-conditioned episodes by relabeling them with goals actually achieved. Recomputes the associated rewards to learn from sparse binary feedback.

## Goal-conditioned representations and planning

- **[Contrastive RL](https://arxiv.org/abs/2206.07568)** — 2022. Contrasts future states with random states for each state–action pair. The optimal critic encodes discounted future-state occupancy ratios; maximizing its score trains a goal-reaching policy.
- **[Search on the Replay Buffer](https://arxiv.org/abs/1906.05253)** — 2019. Builds a graph of visited states with goal-value-based distance estimates, then searches for subgoals a local policy can reach. Planning depends on replay coverage and distance accuracy; evaluated on image navigation.
- **[HIQL](https://arxiv.org/abs/2307.11949)** — 2023. Learns an offline goal-value function, a high-level policy predicting latent subgoals and a low-level controller. Extends IQL to hierarchical goal reaching; value learning can use action-free trajectories, while controller extraction needs actions.
- **[Inference via Interpolation](https://arxiv.org/abs/2403.04082)** — 2024. Its temporal contrastive parameterization yields a Gauss–Markov chain under Gaussian-marginal and optimal-critic assumptions. Infers latent waypoints from offline trajectories; no online control-policy learning.
- **[C-Slerp](https://arxiv.org/abs/2610.20409)** — 2026 preprint. Extends contrastive planning to online RL: rotation-aware spherical interpolation generates latent waypoints and adapts their count. Uses no separate high-level network or graph search. [Code](https://github.com/jonghaepark/c-slerp).
- **[C-Slerp assumptions](https://arxiv.org/html/2610.20409v1#S4.SS3)** — The waypoint derivation assumes a Bayes-optimal critic and uniform spherical marginals, then uses a small-variance approximation. Closed-form latent waypoints do not establish feasible paths for imperfect learned representations.
- **[C-Slerp evidence](https://arxiv.org/html/2610.20409v1#S5.SS1)** — Reports higher success with adaptive than fixed counts on 8-tower and Ant U5 Maze. Five-seed, state-based simulations; eight cubes use direct forces, gripper tasks use up to five. Visual inputs and physical robots remain untested.

## Memory and temporal abstraction

- **[Deep recurrent Q-networks](https://arxiv.org/abs/1507.06527)** — 2015. Adds an LSTM to DQN to integrate observations over time. Studies partial observability and changing observation quality; recurrence does not show a systematic advantage on every fully observed task.
- **[Option-Critic](https://arxiv.org/abs/1609.05140)** — 2016. Learns temporally extended actions through their internal policies and termination rules, together with a policy over options. Does not require externally specified subgoals or extra reward signals.
- **[HIRO](https://arxiv.org/abs/1805.08296)** — 2018. Learns high-level goals and lower-level goal-conditioned control using off-policy data. Corrects higher-level replay for changes in the lower-level behavior that alter what a goal accomplishes.
- **[DIAYN](https://arxiv.org/abs/1802.06070)** — 2018. Learns diverse skills without task rewards using an information-theoretic objective and maximum-entropy policies. Studies skill pretraining and hierarchical composition for later tasks.
- **[Successor features](https://arxiv.org/abs/1606.05312)** — 2016. Separates expected future feature occupancy from reward weights, enabling policy transfer across tasks with shared dynamics and different rewards; paired with generalized policy improvement.

## Learned dynamics and planning

- **[Linear Dyna and prioritized sweeping](https://arxiv.org/abs/1206.3285)** — 2008. Learns from imagined transitions generated by a world model. Extends Dyna planning and prioritized sweeping to linear function approximation, with convergence results under stated conditions.
- **[PETS](https://arxiv.org/abs/1805.12114)** — 2018. Combines probabilistic ensembles of dynamics models with trajectory sampling to propagate uncertainty during planning. Studies model uncertainty as a practical component of data-efficient control.
- **[Model-Based Policy Optimization](https://arxiv.org/abs/1906.08253)** — 2019. Uses short model-generated rollouts branching from real observations. Limits reliance on long simulated trajectories, where accumulated model error can undermine policy optimization.
- **[AlphaZero](https://arxiv.org/abs/1712.01815)** — 2017. Combines neural policy/value prediction, Monte Carlo tree search, and self-play for board games. Uses the game rules for planning; learning without human games does not mean learning without a simulator.
- **[MuZero](https://arxiv.org/abs/1911.08265)** — 2019. Learns a model predicting reward, policy, and value for tree search. Optimizes planning-relevant quantities rather than requiring a model that reconstructs every detail of future observations.
- **[Dreamer](https://arxiv.org/abs/1912.01603)** — 2019. Learns behavior by propagating value gradients through imagined trajectories in a compact latent world model. Separates learning environmental dynamics from collecting every policy update through real interaction.
- **[DreamerV2](https://arxiv.org/abs/2010.02193)** — 2020. Uses discrete latent world-model representations and learns behavior from model predictions. Trains the world model separately from the policy and studies both Atari and continuous control.
- **[DreamerV3](https://arxiv.org/abs/2301.04104)** — 2023. Combines latent imagination with normalization, balancing, and transformation choices intended to stabilize learning across domains. Evaluates a shared configuration across diverse tasks; no universal task guarantee follows.
- **[TD-MPC2](https://arxiv.org/abs/2310.16828)** — 2023. Combines a decoder-free latent world model with local trajectory optimization for continuous control, including multitask training across tasks with different action spaces.

## Learning from fixed datasets

- **[Batch-Constrained Q-learning](https://arxiv.org/abs/1812.02900)** — 2018. Restricts candidate actions to remain close to those supported by a fixed dataset. Addresses extrapolation errors that arise when offline policy learning evaluates poorly supported actions.
- **[Behavior-regularized actor–critic](https://arxiv.org/abs/1911.11361)** — 2019. Organizes offline RL around regularizing policy behavior relative to logged data. Uses shared comparisons and ablations to examine which algorithmic choices matter.
- **[Conservative Q-learning](https://arxiv.org/abs/2006.04779)** — 2020. Adds a value regularizer to Bellman-error training to learn conservative estimates from offline data. Lower-bound results have assumptions; conservative training does not guarantee deployment performance.
- **[Implicit Q-learning](https://arxiv.org/abs/2110.06169)** — 2021. Fits an expectile state-value estimate, backs it into a Q-function, and extracts a policy through advantage-weighted cloning. Avoids querying unseen actions during value learning.
- **[Decision Transformer](https://arxiv.org/abs/2106.01345)** — 2021. Predicts actions autoregressively from desired return, past states, and actions. Recasts offline policy learning as conditional sequence modeling; requesting a return does not guarantee achieving it.
- **[Diffuser](https://arxiv.org/abs/2205.09991)** — 2022. Plans by iteratively denoising trajectories, combining learned generation with conditioning on goals or rewards. Moves part of trajectory optimization into the learned model.
- **[Cal-QL](https://arxiv.org/abs/2303.05479)** — 2023. Calibrates conservative offline value estimates against a reference policy to improve initialization for subsequent online learning; addresses the offline-to-online transition.

## Off-policy evaluation

- **[Sequential doubly robust evaluation](https://arxiv.org/abs/1511.03722)** — 2015/2016. Combines importance weighting with value-model corrections to estimate a target policy’s return from logged behavior. Jiang and Li reduce variance in studied tasks; requires policy probabilities and action support.
- **[Fitted Q Evaluation](https://arxiv.org/abs/1903.08738)** — 2019. Repeatedly regresses Bellman targets for a fixed policy on logged transitions, then estimates its value. Le et al.’s error bounds require coverage and function-class conditions; fitting low regression error alone does not certify a new policy.

## Demonstrations and preference feedback

- **[DAgger](https://arxiv.org/abs/1011.0686)** — 2010. Aggregates expert labels on observations encountered by the learner's policy. Addresses distribution shift between expert demonstrations and the states visited after the learner makes mistakes.
- **[GAIL](https://arxiv.org/abs/1606.03476)** — 2016. Learns a policy through adversarial comparison with expert behavior, without a supplied task reward. The original method still collects policy rollouts; it is not purely offline behavioral cloning.
- **[Human preference rewards](https://arxiv.org/abs/1706.03741)** — 2017. Learns task objectives from human comparisons of trajectory segments and trains policies using that feedback. Replaces hand-written task rewards with learned preferences, not with direct access to human intent.
- **[Learning with demonstrations and long horizons](https://arxiv.org/abs/1805.11593)** — 2018. Combines a transformed Bellman operator, temporal consistency, and human demonstrations for Atari. Separates reward-scale handling, long-horizon learning, and exploration contributions.

## Multiple agents and constrained control

- **[MADDPG](https://arxiv.org/abs/1706.02275)** — 2017. Extends actor–critic learning to account for other agents' actions during training. Studies cooperative and competitive interaction, where other learning agents make the environment nonstationary.
- **[QMIX](https://arxiv.org/abs/1803.11485)** — 2018. Combines per-agent values with a monotonic mixing network for centralized training and decentralized action choice. The monotonicity restriction makes local greedy choices consistent with the joint value model.
- **[Multi-agent RL review](https://arxiv.org/abs/1812.11794)** — 2018. Organizes challenges including nonstationarity, partial observability, communication, and centralized versus decentralized training. Surveys approaches and their application settings.
- **[Constrained Policy Optimization](https://arxiv.org/abs/1705.10528)** — 2017. Optimizes reward subject to expected-cost constraints through a policy-search update. Theoretical near-constraint satisfaction depends on assumptions and does not certify physical safety of a learned controller.
- **[Evolution strategies for control](https://arxiv.org/abs/1703.03864)** — 2017. Optimizes policy parameters through black-box evaluations and perturbations. Provides a control-learning baseline that does not require value functions or policy-gradient credit assignment through actions.

## Evaluation and datasets

- **[Reproducibility in deep RL](https://arxiv.org/abs/1709.06560)** — 2017. Shows how nondeterminism, hyperparameters, and reporting choices complicate algorithm comparisons. Calls for standardized protocols and uncertainty reporting rather than isolated best-run scores.
- **[Arcade Learning Environment protocols](https://arxiv.org/abs/1709.06009)** — 2017. Reviews Atari evaluation practices and introduces sticky actions as environmental stochasticity. Makes protocol differences explicit when comparing game-playing agents.
- **[Statistical uncertainty in RL benchmarks](https://arxiv.org/abs/2108.13264)** — 2021. Shows that few-run point estimates can change conclusions about algorithm rankings. Recommends interval estimates, performance profiles, and robust aggregates such as the interquartile mean.
- **[D4RL](https://arxiv.org/abs/2004.07219)** — 2020. Benchmarks offline learning with human, controller-generated, multitask, and mixed-policy datasets. Tests limitations hidden by datasets collected only from partially trained RL agents.
- **[Off-policy evaluation benchmark](https://arxiv.org/abs/1911.06854)** — 2019. Stress-tests methods that estimate a policy's performance from data collected by other policies. Studies how experimental conditions affect estimator reliability and provides the COBS benchmark.

## Software

- **[Stable-Baselines3](https://www.jmlr.org/papers/v22/20-1364.html)** — 2021. Provides Python implementations with consistent interfaces, documentation, and comparisons to reference codebases. A practical baseline implementation collection; the cited paper describes its tested release.
- **[CleanRL](https://www.jmlr.org/papers/v23/21-1342.html)** — 2022. Provides self-contained algorithm implementations in single files, including training details. Supports inspection and modification of an individual algorithm without tracing a large shared framework.

## Related Topics

- [Neural Networks](https://mlpapers.org/neural-nets/)
- [Optimization](https://mlpapers.org/optimization/)
- [Models](https://mlpapers.org/models/)
