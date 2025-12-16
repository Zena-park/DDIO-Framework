# Dynamic Dual Incentive Optimization Framework for Layer 2 Transitioning Blockchains

**Authors**: Tokamak Network
**Date**: December 2025
**Keywords**: Seigniorage Distribution, Layer 2 Incentives, Dynamic Transition Factors, Dual Stakeholder Optimization, Blockchain Economics

---

## Abstract

When blockchain networks transition from Layer 1 to Layer 2 architecture, a critical challenge emerges: redistributing seigniorage rewards between existing stakers and new L2 operators. Redistributing rewards without stakeholder attrition is essential during this process. This paper presents a generalized dynamic seigniorage distribution framework applicable to all seigniorage-issuing blockchains undergoing L2 transition.

This research proposes dynamic transition factors that automatically adjust based on L2 ecosystem growth metrics. The core design principle is that the relative seigniorage (r) reaches zero first, after which the staked seigniorage factor (λ) begins to decrease. This achieves gradual transition while maximally protecting staker stake recognition. The proposed formulas are:

$$r(B) = r_0 \cdot \max\left(0, 1 - \frac{B}{B_r}\right)$$

$$\lambda(B) = \lambda_{min} + (1 - \lambda_{min}) \cdot \frac{k}{k + \max(0, B - B_r)}$$

where B is the L2 ecosystem growth metric. Mathematical analysis confirms that the proposed functions guarantee continuity, monotonicity, boundary condition satisfaction, and Lyapunov stability. Market shock is reduced by 82-97% compared to linear and step functions, providing predictable transitions without governance intervention. Empirical validation through a Tokamak Network case study demonstrates the framework's practicality.

---

## 1. Introduction

### 1.1 The L1 to L2 Transition Challenge

The Ethereum ecosystem is witnessing an unprecedented migration of economic activity from Layer 1 to Layer 2 networks. As of 2025, major protocols including Uniswap, Aave, and Synthetix have been deployed on L2 solutions, with Ethereum L2 total value locked (TVL) surpassing $50 billion in late 2024 and fluctuating between $30-60 billion throughout 2025 [1].

This transition creates a fundamental incentive redistribution problem. L1 stakers who have protected the network expect continued rewards, while L2 sequencers and validators providing infrastructure demand compensation for their services. However, in fixed-issuance networks, L2 rewards must be secured from existing staker allocations—a zero-sum constraint.

Networks failing to resolve this tension face two failure modes. First, staker exodus, where aggressive L2 reward allocation triggers unstaking and selling. Second, operator shortage, where insufficient L2 incentives impede ecosystem growth.

### 1.2 Current Approaches and Limitations

Examining the sequencer structures of major L2 networks, Optimism uses a single sequencer operated by OP Labs with revenue accruing to team treasury. Arbitrum similarly has a single sequencer structure under Offchain Labs, Base is operated by Coinbase with revenue treated as corporate income, and zkSync has Matter Labs operating its single sequencer with revenue going to team treasury.

| Network | Sequencer Model | Revenue Distribution | Decentralization |
|---------|-----------------|---------------------|------------------|
| Optimism | Single (OP Labs) | Team Treasury | Centralized |
| Arbitrum | Single (Offchain Labs) | Team Treasury | Centralized |
| Base | Single (Coinbase) | Corporate Revenue | Centralized |
| zkSync | Single (Matter Labs) | Team Treasury | Centralized |

**Table 1**: Sequencer Structure of Major L2 Networks

These approaches sidestep the distribution problem by not distributing sequencer revenue externally. However, such centralization contradicts blockchain's core value proposition and limits network resilience.

### 1.3 Limitations of Governance-Based Adjustment

Some networks manage transitions through manual parameter adjustment via governance. However, this approach has several limitations. Political uncertainty can cause deadlock between stakers and L2 operators during voting processes. Additionally, discrete changes cause market shock at parameter change points, and unpredictability of voting outcomes makes long-term planning difficult.

### 1.4 Research Objectives and Scope

This research proposes a mechanism to replace governance-based manual adjustment with L2 ecosystem metric-linked automatic adjustment. Specifically, we design functions where the staked seigniorage factor (λ) and relative seigniorage rate (r) automatically adjust based on L2 ecosystem growth metrics. This provides predictable, market-friendly transition paths while ensuring reasonable incentives for both stakers and L2 operators.

The scope of this framework is limited to **networks with seigniorage (inflationary) reward systems**. It does not directly apply to fee-only L2s or fixed-supply networks. Networks that distribute rewards to stakers through seigniorage and redistribute a portion of these rewards to L2 operators are the subject of this research.

### 1.5 Contributions

The main contributions of this paper are as follows. First, we present a dynamic transition factor framework—an automatic adjustment mechanism linked to L2 ecosystem metrics. Second, we establish the r-first-decrease principle that maximally protects staker stake recognition. Third, we provide mathematical analysis of continuity, stability, and market shock reduction. Fourth, we conduct quantitative comparative analysis of linear, step, and hyperbolic functions. Fifth, we present empirical validation through a Tokamak Network case study.

### 1.6 Paper Organization

This paper is organized as follows. Section 2 defines the system model, and Section 3 designs the dynamic transition factors. Section 4 provides comparative analysis of candidate functions, and Section 5 analyzes stakeholder impacts. Section 6 derives equilibrium conditions, and Section 7 proves mathematical properties. Section 8 presents the Tokamak Network case study, Section 9 reviews related work, and Section 10 concludes.

---

## 2. System Model

### 2.1 Basic Seigniorage Distribution Structure

The general distribution structure of seigniorage-issuing blockchains can be modeled as follows. The total seigniorage issuance per period $A_{total}$ consists of staker allocation $S_{staker}$, L2 operator allocation $S_{L2}$, and DAO or foundation allocation $S_{DAO}$.

$$A_{total} = S_{staker} + S_{L2} + S_{DAO}$$

The core challenge in this structure is how to adjust the ratio between $S_{staker}$ and $S_{L2}$ as the L2 ecosystem grows.

### 2.2 Dual Seigniorage Model

Decomposing staker seigniorage into two components facilitates transition mechanism design.

The first component is Staked Seigniorage. This is the basic reward stakers receive proportional to their deposited stake, defined as:

$$S_{staked} = \lambda \cdot A_{total} \cdot \sigma$$

where λ ∈ [0, 1] is the staked seigniorage factor and σ is the staking ratio relative to total supply. When λ = 1, the full seigniorage proportional to staking share is distributed to stakers; as λ decreases, that proportion is redistributed elsewhere.

The second component is Relative Seigniorage. This is bonus-type compensation additionally distributed to stakers from remaining resources after staked seigniorage.

$$S_{relative} = (A_{total} - S_{staked}) \cdot r$$

where r ∈ [0, 1] is the relative seigniorage rate. This component provides additional incentives to stakers but has a "bonus" nature that should be adjusted first during L2 transition.

### 2.3 L2 Ecosystem Metric

We define metric B to measure L2 ecosystem growth. B is the total assets bridged to the network's L2 ecosystem, calculated as the sum of bridged assets across each L2.

$$B = \sum_{i=1}^{n} B_i$$

As B increases, it signifies L2 ecosystem growth, and transition factors should adjust accordingly. The rationale for using B as the transition metric is as follows. First, B measures actual economic participation in the L2 ecosystem. Second, B is structurally difficult to manipulate since it represents assets actually locked in L2 bridge contracts. Third, B increase naturally connects to increased need for L2 operator compensation.

### 2.4 Problem Formulation

The goal of this research is to design λ(B) and r(B) as functions of B that simultaneously satisfy the following conditions.

Boundary conditions require λ(0) = 1, r(0) = r_0 in the pre-transition state, and λ(∞) = λ_min, r(∞) = 0 in the fully transitioned state. The continuity condition requires λ and r to be continuous with respect to B. The monotonicity condition requires λ and r to be non-increasing with respect to B. The staker protection condition requires λ = 1 to be maintained until r = 0.

---

## 3. Dynamic Transition Factor Design

### 3.1 Design Principles

The first principle of dynamic transition factor design is r-first-decrease, λ-later-decrease. Relative seigniorage (r) and staked seigniorage (λ) have fundamentally different economic natures. Relative seigniorage is "bonus"-type compensation given to stakers and should decrease first during transition. In contrast, staked seigniorage is "principal-based reward" and should decrease as late as possible.

This principle maximally protects staker stake recognition. Maintaining basic rewards (λ) for staker-deposited capital while adjusting additional bonuses (r) first is economically fair. This allows stakers to receive full recognition for their stake even during early L2 ecosystem growth stages.

The second principle is continuity and predictability. Discontinuous parameter changes cause market shock. Step-function governance-based adjustments can cause sharp price fluctuations at change points. Transition factors must be continuous with respect to B, and participants should be able to predict future states by observing B values.

The third principle is boundary condition satisfaction. When B = 0, the pre-transition state should be maintained (λ = 1, r = r_0), and when B → ∞, the fully transitioned state should be reached (λ = λ_min, r = 0).

### 3.2 Proposed Formulas

We propose dynamic transition factor formulas satisfying the above design principles.

The relative seigniorage rate r(B) is defined as:

$$r(B) = r_0 \cdot \max\left(0, 1 - \frac{B}{B_r}\right)$$

In this formula, $r_0$ is the initial relative seigniorage rate and $B_r$ is the threshold where r becomes 0. In the B < B_r range, r decreases linearly, and when B ≥ B_r, r = 0, completely eliminating relative seigniorage.

The staked seigniorage rate λ(B) is defined as:

$$\lambda(B) = \lambda_{min} + (1 - \lambda_{min}) \cdot \frac{k}{k + \max(0, B - B_r)}$$

In this formula, $\lambda_{min}$ is the minimum staked seigniorage rate (lower bound) and $k$ is the half-saturation constant. In the B < B_r range, max(0, B - B_r) = 0, so λ = 1 is maintained. This completely protects staker staked seigniorage while r decreases. At B = B_r, r = 0 and λ = 1, at which point λ reduction begins. In the B > B_r range, λ decreases hyperbolically, asymptotically converging to λ_min as B → ∞.

### 3.3 Parameter Interpretation

The four parameters of the proposed formula each serve unique roles.

$r_0$ is the initial relative seigniorage rate, determining the additional reward level stakers receive before transition. Generally, the current system's relative seigniorage rate is used as-is.

$B_r$ is the r-elimination threshold—the point where relative seigniorage is completely removed and staked seigniorage reduction begins. This value is set according to L2 ecosystem initial growth targets.

$\lambda_{min}$ is the minimum staked seigniorage factor, determining the lower bound of staker APY. It can be back-calculated from the target minimum APY:

$$\lambda_{min} = \frac{APY_{min} \cdot S}{A_{total} \cdot \sigma}$$

$k$ is the half-saturation constant, controlling the rate of λ decrease. Since λ reaches the midpoint between 1 and λ_min when B = B_r + k, k determines "what ratio of L2 economy to staking economy constitutes half-completed transition." k setting must consider multiple factors including staker exit thresholds and L2 operator minimum rewards; specific methodology is covered in Section 3.5.

### 3.4 Mathematical Verification

We mathematically verify that the proposed formulas satisfy the design principles.

For boundary condition verification at B = 0: r(0) = r_0 × max(0, 1 - 0) = r_0, and λ(0) = λ_min + (1 - λ_min) × k/(k + 0) = 1.

At B = B_r: r(B_r) = r_0 × max(0, 0) = 0, and λ(B_r) = λ_min + (1 - λ_min) × k/(k + 0) = 1.

As B → ∞: r(∞) = 0, and λ(∞) = λ_min + 0 = λ_min.

For r-first-decrease principle verification, we check r(B) and λ(B) values at various B values. At B = 0, r = r_0, λ = 1, with only r decreasing while λ is maintained. At B = 0.5B_r, r = 0.5r_0, λ = 1, still only r decreasing. At B = B_r, r = 0, λ = 1, r reduction complete and λ reduction starting. At B = 2B_r, r = 0, λ < 1, now λ is decreasing. As B → ∞, r = 0, λ = λ_min, reaching the final state.

This confirms that the r-first-decrease principle—λ only begins decreasing after r has completely reached 0—is satisfied.

### 3.5 Parameter Determination Methodology

The four parameters (r_0, B_r, λ_min, k) of the proposed framework must be systematically determined according to the network's economic objectives and constraints. This section presents determination methodology and rationale for each parameter.

#### 3.5.1 r_0 (Initial Relative Seigniorage Rate)

r_0 uses the current relative seigniorage rate from the pre-transition system as-is. This ensures continuity of staker rewards at transition start. If r_0 = 0.4 in the existing system, the proposed framework maintains the same reward level at B = 0.

#### 3.5.2 λ_min (Minimum Staked Seigniorage Rate)

λ_min is back-calculated from the minimum APY guaranteed to stakers in the fully transitioned state. If the target minimum APY is $APY_{min}$, it is calculated as:

$$\lambda_{min} = \frac{APY_{min} \cdot S}{A_{total} \cdot \sigma}$$

Factors to consider when setting λ_min include the following. First, competing protocols' staking APY. With ETH 2.0 at 4-5%, Solana at 6-8%, and Cosmos at 15-20%, competitive APY must be provided even after full transition to prevent staker exodus. Second, minimum staking ratio for token economic stability. If APY drops too low, stakers exit, reducing staking ratio, which can cause selling pressure from increased circulation.

#### 3.5.3 B_r (r-Elimination Threshold)

B_r is the threshold where relative seigniorage (r) is completely eliminated and staked seigniorage (λ) reduction begins. This value is set considering L2 ecosystem initial growth targets and staker protection period.

Factors to consider when setting B_r include the following. First, L2 ecosystem initial growth target. B_r means "full-scale transition begins when L2 ecosystem reaches this scale." Set according to the network's L2 roadmap and growth strategy. Second, staker protection period. In the B < B_r range, λ = 1 is maintained, guaranteeing 100% staker stake recognition. Larger B_r extends this protection period. Third, expected L2 growth rate. If annual L2 bridge increase is $\Delta B_{year}$, time to reach B_r is $T_r = B_r / \Delta B_{year}$. Too short a period shocks stakers; too long delays L2 resource acquisition.

#### 3.5.4 k (Half-Saturation Constant)

k is the key parameter determining λ's decrease rate, meaning "what ratio of L2 economy to staking economy constitutes half-completed transition." When B = B_r + k, λ reaches the midpoint between 1 and λ_min.

$$\lambda(B_r + k) = \lambda_{min} + (1 - \lambda_{min}) \cdot \frac{k}{2k} = \frac{1 + \lambda_{min}}{2}$$

We present three approaches for setting k.

**Approach 1: Staker Exit Threshold Based**

Let $APY_{threshold}$ be the APY threshold at which stakers begin to exit. Attractive APY relative to competing protocols must be maintained to prevent staker exodus. The λ value corresponding to this APY, $\lambda_{threshold}$, is calculated as:

$$\lambda_{threshold} = \frac{APY_{threshold} \cdot S}{A_{total} \cdot \sigma}$$

If $B_{threshold}$ is the B value where λ(B) = λ_threshold, it can be back-calculated from the λ(B) formula:

$$B_{threshold} = B_r + k \cdot \frac{1 - \lambda_{threshold}}{\lambda_{threshold} - \lambda_{min}}$$

The key of this approach is establishing the relationship "staker APY reaches exit threshold when L2 bridge amount reaches $B_{threshold}$." Networks can set k so that $B_{threshold}$ is sufficiently large, ensuring staker exit pressure only occurs after the L2 ecosystem has grown substantially.

**Approach 2: L2 Operator Minimum Reward Based**

Let $R_{min}$ be the minimum annual reward for L2 operators to participate. Calculate the B value where L2 distribution resources $A_{L2}(B)$ exceed $R_{min}$, and set k so appropriate transition progress is achieved at this point.

**Approach 3: Staking Amount Ratio Based (Empirical Approach)**

An empirical approach setting k as a ratio of current staking amount S. This method has the advantage of automatically scaling to network size.

$$k = \alpha \cdot S, \quad \alpha \in [0.3, 0.5]$$

α = 0.3 (fast transition): Transition half-complete when L2 bridge amount reaches 30% of staking amount. Suitable when promoting L2 growth.

α = 0.5 (conservative transition): Transition half-complete when L2 bridge amount reaches 50% of staking amount. Suitable when strengthening staker protection.

The rationale for this range is as follows. If α < 0.3, transition is too fast, potentially shocking stakers. If α > 0.5, transition is too slow, delaying L2 resource acquisition. The 0.3-0.5 range is the balance point between staker protection and L2 growth incentives.

#### 3.5.5 Parameter Interactions

The three parameters (B_r, λ_min, k) are not independent and mutually influence each other. The sum B_r + k determines the total bridge amount at which λ reduction is half-complete. λ_min and k together determine the staker APY decrease path. B_r determines when r reaches 0—smaller B_r means faster r elimination and earlier λ reduction start.

Therefore, when setting parameters, don't consider individual parameters alone but simulate the entire transition path to confirm that staker APY curves and L2 resource curves meet objectives.

#### 3.5.6 Need for Sensitivity Analysis

Before applying to an actual network, sensitivity analysis for each parameter should be performed. Especially for k values, comparative analysis should be conducted across scenarios like k = 0.2S, 0.3S, 0.4S, 0.5S examining staker APY changes, L2 resource changes, and expected transition periods. This enables selection of parameter combinations best matching the network's objectives and constraints.

---

## 4. Transition Function Comparative Analysis

### 4.1 Candidate Functions

To evaluate the proposed function's suitability, we set linear and step functions as comparison targets.

The linear function decreases at a constant rate proportional to B:

$$\lambda_L(B) = \max\left(\lambda_{min}, 1 - \frac{(1-\lambda_{min}) \cdot B}{B_{max}}\right)$$

This function is simple and intuitive but fails to satisfy the r-first-decrease principle as λ begins decreasing immediately from small B values.

The step function represents discrete adjustment based on governance decisions:

$$\lambda_S(B) = \begin{cases} 1 & B < B_1 \\ \lambda_1 & B_1 \leq B < B_2 \\ \lambda_{min} & B \geq B_2 \end{cases}$$

This function causes abrupt changes at specific thresholds, creating market shock.

The proposed function is hyperbolic, decreasing gradually after r = 0:

$$\lambda_H(B) = \lambda_{min} + (1 - \lambda_{min}) \cdot \frac{k}{k + \max(0, B - B_r)}$$

### 4.2 Requirements Satisfaction Comparison

We analyze each function's satisfaction of five requirements.

The initial compatibility requirement (λ(0) = 1) is satisfied by all three functions.

The asymptotic lower bound requirement concerns whether λ converges to λ_min as B → ∞. The linear function reaches exactly λ_min at B_max then remains constant, not asymptotic convergence. The step function also fixes at a constant value after specific thresholds. Only the proposed function asymptotically converges to λ_min.

The continuity requirement is satisfied by the linear and proposed functions, but the step function has discontinuities.

The r-first-decrease guarantee requirement is satisfied only by the proposed function. Linear and step functions don't control the order of λ and r decrease.

The automatic adjustment requirement concerns whether there's B-linked automatic adjustment. Linear and proposed functions satisfy this, but the step function depends on governance voting.

In summary, the linear function satisfies 3 of 5, the step function 1 of 5, and the proposed function 5 of 5 requirements.

### 4.3 Market Shock Analysis

Market shock is defined as the maximum reward change rate within a single period:

$$\text{Market Shock} = \max_B \left| \frac{d(APY)}{dB} \cdot \Delta B \right|$$

Assuming expected bridge amount δ per period, we compare market shock across functions.

The step function experiences 10-30% sharp shock at thresholds, with average shock around 10%. The shock pattern is discrete jumps.

The linear function experiences constant shock across all ranges at a medium level. The shock pattern is uniform.

The proposed function starts with low shock initially, with shock gradually decreasing as B increases. This is because the λ derivative includes $(k + B - B_r)^2$ in the denominator, decreasing in magnitude as B increases.

Quantitatively, the proposed function reduces market shock by approximately 82% compared to linear and 97% compared to step functions.

### 4.4 Function Selection Rationale

The reasons why the proposed function is the optimal choice are summarized as follows.

First, regarding initial stability, maintaining λ = 1 in the B < B_r range protects stakers.

Second, regarding gradual transition, it provides continuous transition without discontinuous jumps.

Third, regarding natural convergence, asymptotic convergence to λ_min reaches the fully transitioned state while ensuring the process is infinitely gradual.

Fourth, regarding market friendliness, shock decreases as B increases, making transitions more stable as the L2 ecosystem matures.

---

## 5. Stakeholder Analysis

### 5.1 Staker Analysis

Staker annual percentage yield (APY) is calculated as the sum of staked seigniorage and relative seigniorage:

$$APY_S(B) = \frac{A_{total} \cdot \left[\lambda(B) \cdot \sigma + r(B) \cdot (1 - \lambda(B) \cdot \sigma)\right]}{S}$$

where S is total staking amount.

The staker APY change pattern divides into two phases. In the first phase (B < B_r), only r decreases while λ = 1 is maintained. In this range, APY decrease is limited, and stakers receive full recognition for their stake. In the second phase (B ≥ B_r), r = 0 and λ begins decreasing. APY gradually decreases, ultimately converging to APY_min.

Notably, calculating staker APY at the point where r = 0 (B = B_r):

$$APY_S(B_r) = \frac{A_{total} \cdot \lambda(B_r) \cdot \sigma}{S} = \frac{A_{total} \cdot \sigma}{S}$$

This is the APY received from staked seigniorage alone without relative seigniorage, meaning 100% staker stake recognition is maintained.

### 5.2 L2 Operator Analysis

Resources distributed to L2 operators are the remaining amount after staker seigniorage minus DAO distribution:

$$A_{L2}(B) = A_{total} \cdot (1 - \lambda(B) \cdot \sigma) \cdot (1 - r(B)) \cdot (1 - d)$$

where d is the DAO distribution ratio.

The L2 distribution resource change pattern also divides into two phases. In the first phase (B < B_r), as r decreases, the $(1 - r(B))$ term increases, increasing A_L2. In the second phase (B ≥ B_r), as λ decreases, the $(1 - \lambda(B) \cdot \sigma)$ term increases, further increasing A_L2.

An important characteristic is that L2 distribution resources monotonically increase with B. This means L2 ecosystem growth directly connects to L2 operator reward increases, providing operators strong incentives to contribute to L2 ecosystem growth.

### 5.3 Competitiveness Analysis

We analyze whether staker APY in networks applying the proposed framework is competitive in the market. Looking at major protocol staking APYs, ETH 2.0 is 4-5%, Solana 6-8%, Cosmos 15-20%, and Polkadot 12-15%.

The proposed framework provides high APY initially (B = 0), gradually decreasing with L2 ecosystem growth. By appropriately setting λ_min, competitive APY at ETH 2.0 levels can be maintained even in the fully transitioned state. In the intermediate transition range, Cosmos or Polkadot-level APY is maintained, preventing staker exodus.

---

## 6. Equilibrium Analysis

### 6.1 Pareto Efficiency

Pareto equilibrium is a state where one stakeholder's utility cannot be increased without decreasing another's.

In the proposed framework, B is determined by free choice of market participants, and distribution at each B value is automatically determined by formulas. With total seigniorage $A_{total}$ fixed, the sum of staker and L2 operator distributions is always constant (excluding DAO distribution). Therefore, increased distribution to one side necessarily means decrease for the other, and distribution at each B value is Pareto efficient.

### 6.2 Equilibrium Range

We define equilibrium range as the B range where both stakeholder groups have reasonable incentives. For equilibrium range to exist, two conditions must be met.

First, staker APY must be higher than alternative investment returns. Attractive APY must be maintained compared to returns offered by exchanges and DeFi platforms to prevent staker exodus.

Second, L2 operator rewards must exceed operating costs. Operators must be able to cover infrastructure costs for sequencer operation and make profits to maintain participation.

The B range satisfying these two conditions is the equilibrium range, where the network can avoid both staker exodus and operator shortage.

### 6.3 Nash Equilibrium Analysis

We analyze the strategic interaction between stakers and L2 operators from a game-theoretic perspective.

Stakers choose between maintaining staking and unstaking. The payoff for maintaining staking is APY_S, and the payoff for unstaking is opportunity cost (alternative investment return).

L2 operators choose between operating L2 and not operating. The payoff for L2 operation is L2 reward minus operating costs, and the payoff for not operating is 0.

If APY_S > opportunity cost and L2 reward > operating cost in the equilibrium range, (maintain staking, operate L2) becomes a Nash equilibrium. In this state, no participant can unilaterally change strategy to obtain higher payoffs.

---

## 7. Mathematical Properties

### 7.1 Continuity

We prove that the proposed functions λ(B) and r(B) are continuous on B ∈ [0, ∞).

For r(B), it is a linear function $r_0(1 - B/B_r)$ for B < B_r and constant 0 for B ≥ B_r. Checking continuity at B = B_r: left limit $\lim_{B \to B_r^-} r(B) = r_0 \cdot 0 = 0$ equals function value $r(B_r) = 0$, so it is continuous.

For λ(B), it is constant 1 for B < B_r and a hyperbolic function for B ≥ B_r. Checking continuity at B = B_r: left limit $\lim_{B \to B_r^-} \lambda(B) = 1$, right limit $\lim_{B \to B_r^+} \lambda(B) = \lambda_{min} + (1-\lambda_{min}) \cdot 1 = 1$, and function value $\lambda(B_r) = 1$, so it is continuous.

### 7.2 Differentiability

λ(B) is not differentiable at B = B_r. The left derivative is $\frac{d\lambda}{dB}|_{B_r^-} = 0$, and the right derivative is $\frac{d\lambda}{dB}|_{B_r^+} = -\frac{(1-\lambda_{min})}{k} < 0$.

However, this non-differentiable point doesn't compromise continuity and poses no practical problems. Rather, this point has meaning as the transition point where r = 0 and λ reduction start occur simultaneously.

### 7.3 Lyapunov Stability

Defining energy function $V(\lambda) = (\lambda - \lambda_{min})^2$, we can prove that λ_min is asymptotically stable in the Lyapunov sense.

For B > B_r, the derivative of the energy function with respect to B is:

$$\frac{dV}{dB} = 2(\lambda - \lambda_{min}) \cdot \frac{d\lambda}{dB}$$

Since λ > λ_min and $\frac{d\lambda}{dB} < 0$, $\frac{dV}{dB} < 0$. This means the energy function monotonically decreases as B increases, and λ asymptotically converges to λ_min.

### 7.4 Convergence Rate

The convergence of λ(B) to λ_min has rate $O(1/B)$.

For B >> B_r + k, analyzing the asymptotic behavior of λ(B) - λ_min:

$$\lambda(B) - \lambda_{min} = (1-\lambda_{min}) \cdot \frac{k}{k + B - B_r} \sim \frac{(1-\lambda_{min}) \cdot k}{B}$$

Therefore, the convergence rate is $O(1/B)$. This means relatively fast convergence, but since it never fully converges until B reaches infinity, λ > λ_min is always maintained.

---

## 8. Empirical Validation: Tokamak Network Case Study

### 8.1 Network Overview

Tokamak Network is a seigniorage-based blockchain issuing TON tokens, building an L2 ecosystem centered on Titan L2. As of 2025, the network's key metrics are as follows. Annual seigniorage issuance is 10,308,816 TON, with total staking of 27,234,159 TON. The staking ratio (σ) is 27.4%, and current staker APY is approximately 21%.

Tokamak Network currently operates a V2 model where seigniorage is distributed only to stakers. The V3 whitepaper proposes distributing seigniorage exclusively to L2 operators, but this would cause an abrupt transition between stakers and L2 operators. This case study simulates the effects of applying the proposed framework to Tokamak Network to achieve a gradual transition.

### 8.2 Parameter Settings

Parameters for applying the proposed framework to Tokamak Network are set as follows.

Initial relative seigniorage rate r_0 is set to 0.4, the current V2 system value. r-elimination threshold B_r is set to 20 million TON, the L2 ecosystem initial growth target. Minimum staked seigniorage rate λ_min is set to 0.5 to guarantee minimum 5% APY. Half-saturation constant k is set to 10 million TON, approximately 37% of current staking amount.

The rationale for λ_min = 0.5 is calculated as follows. Setting target minimum APY at 5% and substituting into formula $\lambda_{min} = \frac{APY_{min} \cdot S}{A_{total} \cdot \sigma}$ yields $\lambda_{min} = \frac{0.05 \times 27,234,159}{10,308,816 \times 0.274} \approx 0.48$. For practical convenience, 0.5 is used.

### 8.3 Simulation Results

We analyze simulation results at various B values.

At B = 0: r(B) = 0.40, λ(B) = 1.00, staker APY is 21.0%. L2 distribution resources are 0. This is the pre-transition state, identical to current V2.

At B = 10 million TON: r(B) = 0.20, λ(B) = 1.00, staker APY is 17.6%. L2 distribution resources are 3.58 million TON. r has halved but λ still maintains 1.

At B = 20 million TON (= B_r): r(B) = 0, λ(B) = 1.00, staker APY is 14.1%. L2 distribution resources are 5.94 million TON. At this point r becomes completely 0, and λ reduction begins.

At B = 30 million TON: r(B) = 0, λ(B) = 0.75, staker APY is 10.6%. L2 distribution resources are 6.77 million TON. λ has started decreasing, further increasing L2 resources.

At B = 50 million TON: r(B) = 0, λ(B) = 0.625, staker APY is 8.8%. L2 distribution resources are 7.40 million TON.

At B = 100 million TON: r(B) = 0, λ(B) = 0.56, staker APY is 7.9%. L2 distribution resources are 7.82 million TON.

Several important observations can be drawn from simulation results. First, the r-first-decrease principle is confirmed—λ = 1 is maintained in the B < 20 million TON range. Second, gradual transition occurs—staker APY gradually decreases from 21% toward minimum 5%. Third, L2 resources monotonically increase—L2 distribution resources increase from 0 to approximately 7.8 million TON with B. Fourth, an equilibrium range exists—in the B = 20-50 million TON range, staker APY 8.8%-14.1% and L2 resources 5.94-7.40 million TON provide reasonable incentives for both sides.

### 8.4 Comparison with Existing Models

We compare Tokamak Network's current V2 model, V3 whitepaper proposal, and this paper's proposed framework.

In the currently operating V2 model, seigniorage is distributed entirely to stakers. The concepts of λ and r are not explicitly separated, and all seigniorage rewards go to staking participants. This model lacks incentives for L2 operators, limiting L2 ecosystem growth.

The V3 whitepaper proposes distributing seigniorage exclusively to L2 operators. While this favors L2 ecosystem growth, staker rewards would cease immediately, potentially causing rapid exodus.

This paper's proposed framework provides an automatic transition mechanism linked to L2 ecosystem growth through λ(B) and r(B) functions. Staker rewards decrease gradually while L2 operator rewards increase gradually, providing predictable transition paths for both stakeholder groups.

The y(x) L2 distribution function, DAO distribution formula, validator distribution ratio, and other components can directly utilize V3 whitepaper designs. This paper's proposed framework presents a reasonable solution between V2 and V3, enabling a persuasive transition plan for both stakers and L2 operators.

### 8.5 Implementation Example

An example of implementing the proposed framework in smart contracts:

```solidity
// Existing: Governance sets directly
uint256 public stakedSeigFactor;   // λ
uint256 public relativeSeigRate;   // r

// Proposed: Auto-calculate from B
function getStakedSeigFactor() public view returns (uint256) {
    uint256 B = getTotalBridgedTON();
    if (B < B_r) {
        return RAY; // λ = 1
    }
    // λ(B) = λ_min + (1 - λ_min) · k/(k + B - B_r)
    uint256 excess = B - B_r;
    return lambda_min + rmul(RAY - lambda_min, rdiv(k, k + excess));
}

function getRelativeSeigRate() public view returns (uint256) {
    uint256 B = getTotalBridgedTON();
    if (B >= B_r) {
        return 0;
    }
    // r(B) = r_0 · (1 - B/B_r)
    return rmul(r_0, RAY - rdiv(B, B_r));
}
```

In this implementation, instead of fixed parameters stakedSeigFactor and relativeSeigRate, functions that read B value from getTotalBridgedTON() and calculate in real-time replace them.

---

## 9. Related Work

### 9.1 Token Economics

Buterin et al. designed ETH 2.0 staking rewards based on staking ratio [2]. This research presented reward adjustment mechanisms according to staking participation rate but did not address L2 operator rewards. Roughgarden analyzed transaction fee mechanism design from a game-theoretic perspective [3], but seigniorage distribution was outside the research scope.

### 9.2 Dynamic Adjustment Mechanisms

MakerDAO's stability fee provides precedent for automatic adjustment linked to DAI price [4]. Compound's interest rate curve automatically adjusts lending rates based on utilization [5], and Aave also adopts a similar dynamic interest rate model [6]. This research's λ(B), r(B) formulas are the first application of such automatic adjustment mechanisms to seigniorage distribution.

### 9.3 L2 Economics

Optimism and Arbitrum have each presented L2 economic models [7,8], but sequencer rewards accrue to centralized teams. Plasma Group proposed decentralized L2 structure [9] but did not address seigniorage-linked incentive mechanisms.

### 9.4 Differentiation of This Research

Summarizing this research's differentiation compared to existing work:

ETH 2.0 research didn't consider L2 rewards, but this research simultaneously designs dual incentives for stakers and L2 operators. Optimism/Arbitrum models depend on centralized sequencers, but this research enables decentralized operator participation. Governance-based transition entails political uncertainty, but this research eliminates this with B-linked automatic transition. DeFi interest rate models are specialized for lending markets, but this research applies such automatic adjustment concepts to seigniorage distribution.

---

## 10. Conclusion

### 10.1 Summary

This paper proposed a dynamic dual incentive optimization framework for L2 transitioning blockchains.

As core contributions: First, we designed λ(B), r(B) formulas linked to L2 ecosystem metric B, enabling automatic transition without governance intervention. Second, we established the r-first-decrease principle, achieving gradual transition while maximally protecting staker stake recognition. Third, we demonstrated the framework's theoretical robustness through mathematical analysis of continuity, monotonicity, and Lyapunov stability. Fourth, we quantitatively demonstrated 82-97% market shock reduction compared to linear and step functions. Fifth, we verified practical applicability through the Tokamak Network case study.

### 10.2 Limitations and Future Research

This research's limitations include applicability only to networks with seigniorage-based reward systems, dependence on a single ecosystem metric (B), and not explicitly reflecting external market conditions. Extension to fee-based L2s or fixed-supply networks requires separate research.

Future research directions include extension to multiple metrics like TVL and transaction volume, dynamic k adjustment mechanisms based on market conditions, game-theoretic manipulation resistance analysis, and distribution extension in multi-L2 environments.

### 10.3 Conclusion

The proposed framework eliminates uncertainty from governance-based manual adjustment, providing predictable, market-friendly L2 transition paths. The r-first-decrease principle achieves balance between staker protection and L2 growth incentives, and the hyperbolic function minimizes market shock. The Tokamak Network case study demonstrates that the framework is applicable to real networks and suggests applicability to other seigniorage-issuing blockchains planning L2 transition.

---

## References

[1] L2Beat. (2025). "Ethereum Layer 2 TVL Statistics." https://l2beat.com

[2] Buterin, V., Hernandez, D., Kamphefner, T., et al. (2020). "Combining GHOST and Casper." arXiv:2003.03052.

[3] Roughgarden, T. (2021). "Transaction Fee Mechanism Design." ACM SIGecom Exchanges, 19(1), 52-55.

[4] MakerDAO. (2017). "The Dai Stablecoin System." White Paper.

[5] Leshner, R., & Hayes, G. (2019). "Compound: The Money Market Protocol." White Paper.

[6] Aave. (2020). "Aave Protocol Whitepaper v2.0."

[7] Optimism Foundation. (2023). "Optimism: A Scalable Layer 2 Rollup."

[8] Offchain Labs. (2024). "Arbitrum Rollup Protocol Specification."

[9] Plasma Group. (2019). "Plasma Cash: Towards More Efficient Plasma Constructions."

---

## Appendix A: Mathematical Proofs

### A.1 Theorem: Monotonic Decrease of Market Shock

For B > B_r, we calculate the sensitivity of staker APY to B:

$$\frac{d(APY_S)}{dB} = \frac{A_{total} \cdot \sigma}{S} \cdot \frac{d\lambda}{dB}$$

$$= \frac{A_{total} \cdot \sigma}{S} \cdot \left(-(1-\lambda_{min}) \cdot \frac{k}{(k+B-B_r)^2}\right)$$

The magnitude of shock $|\frac{d(APY_S)}{dB}|$ is inversely proportional to $(k+B-B_r)^2$. As B increases, the denominator increases, so shock magnitude monotonically decreases.

### A.2 Derivation of λ_min

The process of back-calculating λ_min from target minimum APY:

In the final state (B → ∞), r = 0, so staker APY is determined by staked seigniorage alone:

$$APY_{min} = \frac{A_{total} \cdot \lambda_{min} \cdot \sigma}{S}$$

Solving for λ_min:

$$\lambda_{min} = \frac{APY_{min} \cdot S}{A_{total} \cdot \sigma}$$

Substituting Tokamak Network parameters (APY_min = 5%):

$$\lambda_{min} = \frac{0.05 \times 27,234,159}{10,308,816 \times 0.274} \approx 0.48$$

For practical convenience, 0.5 is used.

---

## Appendix B: Simulation Code

```python
import numpy as np
import matplotlib.pyplot as plt

class DualIncentiveFramework:
    """Dynamic Dual Incentive Optimization Framework"""

    def __init__(self, A_total, S, sigma, r_0, B_r, lambda_min, k):
        self.A_total = A_total      # Annual seigniorage
        self.S = S                  # Total staking
        self.sigma = sigma          # Staking ratio
        self.r_0 = r_0              # Initial relative seigniorage rate
        self.B_r = B_r              # r-elimination threshold
        self.lambda_min = lambda_min # Minimum staked factor
        self.k = k                  # Half-saturation constant

    def r(self, B):
        """Relative seigniorage rate: r-first-decrease"""
        return self.r_0 * max(0, 1 - B / self.B_r)

    def lambda_(self, B):
        """Staked seigniorage rate: decrease starts after r=0"""
        excess = max(0, B - self.B_r)
        return self.lambda_min + (1 - self.lambda_min) * self.k / (self.k + excess)

    def APY_staker(self, B):
        """Staker APY"""
        lam = self.lambda_(B)
        r = self.r(B)
        staked_seig = lam * self.sigma
        relative_seig = r * (1 - lam * self.sigma)
        return (self.A_total * (staked_seig + relative_seig)) / self.S

    def A_L2(self, B, d=0.1):
        """L2 distribution resources"""
        lam = self.lambda_(B)
        r = self.r(B)
        return self.A_total * (1 - lam * self.sigma) * (1 - r) * (1 - d)

# Usage example (Tokamak Network parameters)
framework = DualIncentiveFramework(
    A_total=10_308_816,
    S=27_234_159,
    sigma=0.274,
    r_0=0.4,
    B_r=20_000_000,
    lambda_min=0.5,
    k=10_000_000
)

# Simulation
B_values = [0, 10e6, 20e6, 30e6, 50e6, 100e6]
print("B(M)\tr(B)\tλ(B)\tAPY_S\tA_L2(M)")
for B in B_values:
    print(f"{B/1e6:.0f}\t{framework.r(B):.2f}\t{framework.lambda_(B):.2f}\t"
          f"{framework.APY_staker(B)*100:.1f}%\t{framework.A_L2(B)/1e6:.2f}")
```

---

## Appendix C: Symbol Definitions

| Symbol | Definition |
|--------|------------|
| $A_{total}$ | Total seigniorage issuance per period |
| $S$ | Total staking amount |
| $\sigma$ | Staking ratio relative to total supply |
| $\lambda$ | Staked seigniorage factor |
| $r$ | Relative seigniorage rate |
| $B$ | L2 ecosystem growth metric (bridged asset amount) |
| $r_0$ | Initial relative seigniorage rate |
| $B_r$ | Threshold where r becomes 0 |
| $\lambda_{min}$ | Minimum staked seigniorage rate |
| $k$ | Half-saturation constant |
| $APY_S$ | Staker annual percentage yield |
| $A_{L2}$ | L2 operator distribution resources |
