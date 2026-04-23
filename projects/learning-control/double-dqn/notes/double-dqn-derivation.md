---
layout: project
title: Double DQN Derivation
project: double-dqn
project_title: Double DQN
category: learning-control
kind: note
date: 2025-05-17
order: 1
summary: Derives mathematically how double deep Q-learning trains. 
permalink: /projects/learning-control/double-dqn/notes/double-dqn-overestimation/
---

## Purpose

The main aim is to explain:

1. The Bellman equations behind Q-learning.
2. Why the classical DQN target has an overestimation tendency.
3. How Double DQN modifies the target.
4. How target networks, replay, and epsilon-greedy exploration fit together.

## Markov decision process and Q-functions

We begin with a discounted Markov decision process

\[
(\mathcal{S}, \mathcal{A}, P, r, \gamma),
\]

where:

- \( \mathcal{S} \) is the state space,
- \( \mathcal{A} \) is the action space,
- \( P(\cdot \mid s,a) \) is the transition kernel,
- \( r(s,a) \) is the one-step reward,
- \( \gamma \in [0,1) \) is the discount factor.

In this situation, the action set is discrete:

\[
\mathcal{A} = \{-1,+1\},
\]

with \(-1\) interpreted as pushing left and \(+1\) as pushing right.

### Policy

A policy is a map \( \pi(a \mid s) \) assigning probabilities to actions given state.

### State-value and action-value functions

For a policy \( \pi \), define

\[
V^\pi(s)
=
\mathbb{E}^\pi \left[
\sum_{k=0}^{\infty} \gamma^k r_{t+k}
\;\middle|\;
s_t = s
\right]
\]

and

\[
Q^\pi(s,a)
=
\mathbb{E}^\pi \left[
\sum_{k=0}^{\infty} \gamma^k r_{t+k}
\;\middle|\;
s_t = s,\; a_t = a
\right].
\]

The optimal action-value function is

\[
Q^\ast(s,a) = \sup_\pi Q^\pi(s,a).
\]

A greedy policy with respect to a Q-function is

\[
\pi_Q(s) \in \arg\max_{a \in \mathcal{A}} Q(s,a).
\]

## Bellman equations

The Bellman optimality equation for \( Q^\ast \) is

\[
Q^\ast(s,a)
=
r(s,a)
+
\gamma \, \mathbb{E}_{s' \sim P(\cdot\mid s,a)}
\left[
\max_{a' \in \mathcal{A}} Q^\ast(s',a')
\right].
\]

This motivates the Bellman optimality operator \( T \), defined by

\[
(TQ)(s,a)
=
r(s,a)
+
\gamma \, \mathbb{E}_{s' \sim P(\cdot\mid s,a)}
\left[
\max_{a' \in \mathcal{A}} Q(s',a')
\right].
\]

### Contraction theorem

The Bellman optimality operator \( T \) is a contraction on the space of bounded functions
\( Q : \mathcal{S}\times\mathcal{A} \to \mathbb{R} \), equipped with the sup norm

\[
\|Q\|_\infty = \sup_{s,a} |Q(s,a)|.
\]

More precisely,

\[
\|TQ_1 - TQ_2\|_\infty
\le
\gamma \|Q_1 - Q_2\|_\infty.
\]

### Proof

Let \( Q_1,Q_2 \) be bounded. For any \( (s,a) \),

\[
(TQ_1)(s,a) - (TQ_2)(s,a)
=
\gamma
\mathbb{E}_{s'}
\left[
\max_{a'} Q_1(s',a') - \max_{a'} Q_2(s',a')
\right].
\]

Taking absolute values and using \( |\mathbb{E}[X]| \le \mathbb{E}[|X|] \),

\[
\left|(TQ_1)(s,a) - (TQ_2)(s,a)\right|
\le
\gamma
\mathbb{E}_{s'}
\left[
\left|
\max_{a'} Q_1(s',a') - \max_{a'} Q_2(s',a')
\right|
\right].
\]

Now use the elementary inequality

\[
\left|
\max_i u_i - \max_i v_i
\right|
\le
\max_i |u_i - v_i|.
\]

Hence

\[
\left|(TQ_1)(s,a) - (TQ_2)(s,a)\right|
\le
\gamma
\mathbb{E}_{s'}
\left[
\max_{a'} |Q_1(s',a') - Q_2(s',a')|
\right]
\le
\gamma \|Q_1 - Q_2\|_\infty.
\]

Taking the supremum over \( (s,a) \) yields

\[
\|TQ_1 - TQ_2\|_\infty
\le
\gamma \|Q_1 - Q_2\|_\infty.
\]

### Corollary

There exists a unique fixed point \( Q^\ast \) such that

\[
TQ^\ast = Q^\ast.
\]

This fixed point is the optimal action-value function.

## Classical Q-learning and DQN

If the state-action space is small, one may update a table by

\[
Q_{t+1}(s_t,a_t)
=
Q_t(s_t,a_t)
+
\alpha_t
\left[
r_t + \gamma \max_{a'} Q_t(s_{t+1},a') - Q_t(s_t,a_t)
\right].
\]

Deep Q-learning replaces the table by a neural network \( Q_\theta(s,a) \), or in discrete-action form a network

\[
Q_\theta(s)
=
\begin{bmatrix}
Q_\theta(s,a_1) & \cdots & Q_\theta(s,a_m)
\end{bmatrix}.
\]

For a sampled transition \( (s,a,r,s',d) \), where \( d \in \{0,1\} \) is the terminal indicator, the classical DQN target is

\[
Y^{\mathrm{DQN}}
=
r + \gamma (1-d)\max_{a'} Q_{\theta^-}(s',a').
\]

Here \( \theta^- \) denotes the target-network parameters.

The corresponding regression objective is

\[
\mathcal{L}(\theta)
=
\mathbb{E}\left[
\ell\left(
Q_\theta(s,a),\, Y^{\mathrm{DQN}}
\right)
\right],
\]

where \( \ell \) is typically squared loss or Huber loss.

## Why the max operator induces overestimation

The important difficulty is that maximisation and noisy estimation do not commute well.

### Proposition

Let \( X_1,\dots,X_m \) be integrable random variables. Then

\[
\mathbb{E}\left[\max_{1\le i\le m} X_i\right]
\ge
\max_{1\le i\le m} \mathbb{E}[X_i].
\]

### Proof

For each \( i \),

\[
\max_j X_j \ge X_i.
\]

Taking expectations gives

\[
\mathbb{E}\left[\max_j X_j\right] \ge \mathbb{E}[X_i].
\]

Since this holds for every \( i \),

\[
\mathbb{E}\left[\max_j X_j\right] \ge \max_i \mathbb{E}[X_i].
\]

Now suppose the estimated next-state Q-values are

\[
\widehat{Q}(s',a) = Q^\ast(s',a) + \varepsilon_a,
\qquad
\mathbb{E}[\varepsilon_a] = 0.
\]

Even if each estimator is unbiased for each action separately, we still have

\[
\mathbb{E}\left[\max_a \widehat{Q}(s',a)\right]
\ge
\max_a Q^\ast(s',a).
\]

Thus the \( \max \) applied to noisy estimates introduces an upward tendency.

This does not mean every individual target is too large. It means the maximisation step has a built-in optimistic bias on average when the same noisy estimator is used both to choose and to evaluate the action.

## Double DQN

Double DQN separates:

1. action selection,
2. action evaluation.

Instead of using the target network for both, it uses the online network to choose the action and the target network to evaluate that chosen action. The Double DQN target is

\[
Y^{\mathrm{DDQN}}
=
r
+
\gamma (1-d)\,
Q_{\theta^-}\left(
s',
\arg\max_{a'} Q_\theta(s',a')
\right).
\]

### Interpretation

The online network answers

\[
a^\ast_{\text{online}}(s') \in \arg\max_{a'} Q_\theta(s',a').
\]

The target network then answers

\[
Q_{\theta^-}(s', a^\ast_{\text{online}}(s')).
\]

So the noisy maximisation is no longer performed on the same set of values used for evaluation.

### Proposition

If \( a_\theta(s') \) denotes the greedy action selected by the online network, then the Double DQN target can be written as

\[
Y^{\mathrm{DDQN}}
=
r + \gamma (1-d)\, Q_{\theta^-}(s', a_\theta(s')).
\]

This is a Bellman-style target with decoupled selector and evaluator.

### Proof

By definition,

\[
a_\theta(s') \in \arg\max_{a'} Q_\theta(s',a').
\]

Substituting this into the Double DQN formula gives the stated expression directly.

Double DQN reduces the specific overestimation mechanism caused by taking a maximum over a single noisy estimator. It does not eliminate all approximation error, optimisation error, or sampling error.

## Loss function and gradient step

We use the Smooth L1 loss, that is, the Huber-type loss

\[
\mathcal{L}(\theta)
=
\mathbb{E}\left[
\rho\left(
Q_\theta(o,a) - Y^{\mathrm{DDQN}}
\right)
\right],
\]

where \( o \) denotes the network input and \( \rho \) is the Huber penalty.

For a minibatch \( \{(o_i,a_i,r_i,o_i',d_i)\}_{i=1}^B \), the empirical objective is

\[
\widehat{\mathcal{L}}(\theta)
=
\frac{1}{B}
\sum_{i=1}^B
\rho\left(
Q_\theta(o_i,a_i) - y_i
\right),
\]

with

\[
y_i
=
r_i
+
\gamma (1-d_i)\,
Q_{\theta^-}\left(
o_i',
\arg\max_{a'} Q_\theta(o_i',a')
\right).
\]

We also clip the temporal-difference target:

\[
y_i \leftarrow \operatorname{clip}(y_i,\; y_{\min},\; y_{\max}).
\]

After backpropagation, the gradient norm is clipped.

Target clipping and gradient clipping are stabilisation devices. They are not part of the Bellman theory itself, but they are often useful in practice.

## Target networks

We keep two networks:

1. an online network with parameters \( \theta \),
2. a target network with parameters \( \theta^- \).

Initially, the target network is copied from the online network:

\[
\theta^-_0 = \theta_0.
\]

Two update styles are common.

### Hard updates

A hard update every \( N \) optimiser steps is

\[
\theta^- \leftarrow \theta.
\]

This is piecewise constant in time. Between hard updates, the target network does not move.

### Soft updates

A soft update, also called Polyak averaging, is

\[
\theta^- \leftarrow \tau \theta + (1-\tau)\theta^-,
\qquad
0 < \tau \ll 1.
\]

### Proposition

After one soft update step,

\[
\theta^-_{\text{new}} - \theta
=
(1-\tau)(\theta^-_{\text{old}} - \theta).
\]

So the target network moves a fraction \( \tau \) towards the online network.

### Proof

Starting from

\[
\theta^-_{\text{new}} = \tau \theta + (1-\tau)\theta^-_{\text{old}},
\]

subtract \( \theta \) from both sides:

\[
\theta^-_{\text{new}} - \theta
=
\tau \theta + (1-\tau)\theta^-_{\text{old}} - \theta
=
(1-\tau)\theta^-_{\text{old}} - (1-\tau)\theta
=
(1-\tau)(\theta^-_{\text{old}} - \theta).
\]

We currently use both mechanisms, but you may use hard copying rather than Polyak averaging.

## Experience replay

Instead of training on consecutive transitions, DQN stores transitions in a replay buffer and samples minibatches from it.

Let the buffer at time \( t \) be

\[
\mathcal{B}_t = \{z_1,\dots,z_M\},
\qquad
z_i = (o_i,a_i,r_i,o_i',d_i).
\]

Then the training step uses a sampled minibatch

\[
\{z_{i_1},\dots,z_{i_B}\} \subset \mathcal{B}_t.
\]

The theoretical purpose is to reduce temporal correlation and improve reuse of data.

We also include an action-balancing heuristic. This is a practical sampling modification rather than a standard part of the classical DQN theorem.

## Epsilon-greedy exploration

The policy used for data collection is epsilon-greedy:

\[
a_t
=
\begin{cases}
\text{random action}, & \text{with probability } \epsilon_t, \\
\arg\max_{a} Q_\theta(o_t,a), & \text{with probability } 1-\epsilon_t.
\end{cases}
\]

A common decay rule is

\[
\epsilon_{t+1} = \epsilon_t \eta,
\]

until a minimum value is reached.

## CartPole model

The environment state is

\[
s_t =
\begin{bmatrix}
x_t \\
\theta_t \\
\dot{x}_t \\
\dot{\theta}_t
\end{bmatrix}
\in \mathbb{R}^4.
\]

Here:

- \( x_t \) is cart position,
- \( \theta_t \) is pole angle,
- \( \dot{x}_t \) is cart velocity,
- \( \dot{\theta}_t \) is angular velocity.

The action is a signed horizontal force

\[
F_t = a_t F_{\max},
\qquad
a_t \in \{-1,+1\}.
\]

With

\[
m_c = \text{cart mass}, \qquad
m_p = \text{pole mass}, \qquad
l = \text{half pole length},
\]

the implemented continuous-time accelerations are

\[
\operatorname{temp}
=
\frac{F_t + m_p l \dot{\theta}_t^2 \sin\theta_t}{m_c + m_p},
\]

\[
\ddot{\theta}_t
=
\frac{
g \sin\theta_t - \cos\theta_t\, \operatorname{temp}
}{
l\left(
\frac{4}{3} - \frac{m_p \cos^2\theta_t}{m_c + m_p}
\right)
},
\]

and

\[
\ddot{x}_t
=
\operatorname{temp}
-
\frac{m_p l \ddot{\theta}_t \cos\theta_t}{m_c + m_p}.
\]

### Euler discretisation

We advance the system by explicit Euler updates:

\[
\dot{x}_{t+1} = \dot{x}_t + \ddot{x}_t \Delta t,
\qquad
\dot{\theta}_{t+1} = \dot{\theta}_t + \ddot{\theta}_t \Delta t,
\]

\[
x_{t+1} = x_t + \dot{x}_{t+1}\Delta t,
\qquad
\theta_{t+1} = \theta_t + \dot{\theta}_{t+1}\Delta t.
\]

### Proposition

These updates define a deterministic discrete-time transition map

\[
s_{t+1} = f(s_t,a_t).
\]

Therefore, if the full four-dimensional state is observed, the environment is Markov.

### Proof

Each component of \( s_{t+1} \) is an explicit function of \( s_t \) and \( a_t \) only, via the acceleration formulas and Euler integration. Hence the next state depends on no earlier history once \( (s_t,a_t) \) is known.

## Reward and termination

Termination occurs when the cart or pole leaves the allowed range:

\[
|x_t| > x_{\max}
\quad \text{or} \quad
|\theta_t| > \theta_{\max}.
\]

If termination occurs, the reward is set to a clipped minimum value.

Otherwise, the shaped reward has the form

\[
r_t
=
1
-
0.7 \frac{|\theta_t|}{\theta_{\max}}
-
0.3 \min\left(\frac{|\dot{\theta}_t|}{\dot{\theta}_{\max}},\,1\right)
-
0.1 |\dot{\theta}_t|,
\]

followed by extra multiplicative penalties near the angular threshold and then final clipping.

### Proposition

The implemented one-step reward is bounded.

### Proof

The code performs explicit clipping

\[
r_t \in [r_{\min}, r_{\max}],
\]

with finite constants \( r_{\min} \) and \( r_{\max} \). Therefore the reward is bounded by construction.

## CartPole network

For the abstract theory above, one can write the network input as \( o_t \). This keeps the Bellman equations clean.

For this project, we distinguish between the full environment state \( s_t \) and the two-dimensional network input.

### Observation map seen by the network

Let

\[
o_t = \phi(s_t) \in \mathbb{R}^2
\]

denote the vector supplied to the Q-network.

### Acting-time map

When the agent chooses an action, it extracts

\[
(state[2], state[3]) = (\dot{x}_t, \dot{\theta}_t),
\]

and normalises by

\[
\left(
\frac{\dot{x}_t}{\theta_{\max}},
\frac{\dot{\theta}_t}{\dot{\theta}_{\max}}
\right).
\]

So the first coordinate sent to the network is the cart velocity, but it is scaled by the angular threshold \( \theta_{\max} \).

### Training-time map

During training, the trainer normalises the last two entries of the stored state and then applies \( \tanh \):

\[
\phi_{\text{train}}(s_t)
=
\tanh
\begin{bmatrix}
\dot{x}_t / \theta_{\max} \\
\dot{\theta}_t / \dot{\theta}_{\max}
\end{bmatrix}.
\]

### Diagnostic map

The diagnostic Q-grid is evaluated over

\[
(\theta,\dot{\theta})
\]

with linear normalisation

\[
\phi_{\text{diag}}(\theta,\dot{\theta})
=
\begin{bmatrix}
\theta / \theta_{\max} \\
\dot{\theta} / \dot{\theta}_{\max}
\end{bmatrix}.
\]

This means there are three distinct input conventions in play:

1. action-time input,
2. training-time input,
3. diagnostic-time input.

So one must be careful not to describe the project as if it were a clean two-state \( (\theta,\dot{\theta}) \) learner from end to end.

Because the full physical process is Markov in \( s_t \in \mathbb{R}^4 \) but the network only receives a two-dimensional projection \( o_t \), the learning problem is better viewed as control under reduced observation. In general, \( o_t \) alone need not be Markov.

## Double DQN target

To match the implementation, let the stored transition be

\[
(o_i, a_i, r_i, o_i', d_i),
\]

where \( a_i \in \{0,1\} \) indexes the two output neurons.

The online network outputs

\[
Q_\theta(o_i) =
\begin{bmatrix}
Q_\theta(o_i,0) & Q_\theta(o_i,1)
\end{bmatrix},
\]

and the selected action-value is obtained by gathering the chosen component:

\[
Q_\theta(o_i,a_i).
\]

The next action is chosen by the online network:

\[
a_i^\ast
=
\arg\max_{a' \in \{0,1\}} Q_\theta(o_i',a').
\]

The target network then evaluates that chosen action:

\[
Q_{\theta^-}(o_i', a_i^\ast).
\]

Hence the implemented target is

\[
y_i
=
r_i
+
\gamma (1-d_i)
Q_{\theta^-}(o_i', a_i^\ast).
\]

This is exactly the Double DQN rule.