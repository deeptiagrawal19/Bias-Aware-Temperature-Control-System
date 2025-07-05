# Mitigating Gender Bias in AI-Powered Climate Control: A Reinforcement Learning Approach

This project demonstrates how gender bias can manifest in AI-driven climate control systems and presents a fairness-aware reinforcement learning solution to address it. It highlights the stark difference in thermal comfort between male and female occupants when an AI is trained on biased data and showcases how explicitly designing for fairness can lead to more equitable and satisfactory outcomes for everyone.

This work is directly inspired by the critical discussion in the *Towards Data Science* article, **["Why We Should Focus on AI for Women"](https://towardsdatascience.com/why-we-should-focus-on-ai-for-women/)**. The article compellingly argues that AI systems trained on non-representative data can lead to significant performance disparities and harmful outcomes, a problem this simulation brings to life in the context of thermal comfort.

The thermal comfort models and gender-specific preferences used in this simulation are conceptually based on patterns observed in the **[ASHRAE Global Thermal Comfort Database II](https://www.kaggle.com/datasets/claytonmiller/ashrae-global-thermal-comfort-database-ii)**, a comprehensive collection of indoor environmental quality data.

---

## The Problem: An AI That Only Works for Men

Historically, office and building temperature standards have been based on the metabolic rate of an average 40-year-old man. This has resulted in environments that are often uncomfortably cold for female occupants. When this historical bias is used to train an AI for an automated HVAC system, it doesn't just perpetuate the problem—it encodes and automates it.

Our simulation models this exact scenario with a **"Biased (Male-only)"** agent. This Q-learning agent is trained with the single goal of maximizing the thermal comfort of male occupants (optimal temperature ~22°C). The result is an AI that learns to keep the room cool, achieving high satisfaction for men but completely failing to meet the needs of women (optimal temperature ~24°C).

## The Solution: Designing for Fairness

To counteract this bias, we developed and evaluated two alternative reinforcement learning agents designed with fairness and inclusivity in mind:

1.  **Hybrid Adaptive Agent**: This agent is trained using a blended reward signal that is a weighted average of the comfort scores of both male and female occupants. It learns to find a compromise temperature that balances the needs of the entire population.
2.  **Fairness-Aware Agent**: This agent takes a more direct approach. Its reward function is explicitly engineered to maximize overall comfort *while penalizing* the disparity (or "fairness gap") between male and female comfort scores. It is incentivized not just to make people comfortable, but to do so equitably.

---

## Experimental Results & Analysis

We ran a comprehensive experiment evaluating the three agents across various simulated office populations (with male population ratios of 30%, 50%, and 70%). The results are unequivocal: designing for fairness works.

### Key Findings:

* Fairness Gap Reduction : The Biased agent creates a massive fairness gap (over 0.5). Both the Hybrid and Fairness-Aware agents reduce this gap dramatically. The **Fairness-Aware agent virtually eliminates the gap**, bringing it down to just ~0.05, demonstrating its superior ability to create an equitable environment.

*  Satisfaction Rates : This is the most telling result. In a balanced 50/50 population, the Biased agent results in a **~95% satisfaction rate for men but a near 0% rate for women**. In stark contrast, the **Fairness-Aware agent achieves over 85% satisfaction for *both* genders**. It finds a solution that serves everyone.

*  Temperature Distribution : The agents' learned behaviors are clear. The Biased agent consistently targets a temperature around 22°C. The Hybrid and Fairness-Aware agents learn to maintain a temperature closer to **23.5°C**, a much more inclusive middle ground that accommodates the preferences of both groups.

*  Overall System Accuracy : Crucially, introducing fairness does not compromise performance. Both the Hybrid and Fairness-Aware agents achieve a higher overall system accuracy than the Biased agent, proving that **fairness and effectiveness are not mutually exclusive**.

* Bias Reduction Impact : The Fairness-Aware model consistently achieves a **~90% improvement in fairness** (reduction in the fairness gap) compared to the biased model, regardless of the population's gender ratio.

---

## How to Run the Simulation

The entire experiment is self-contained in the provided Python script.

1.  Ensure you have the required libraries installed: `numpy`, `pandas`, `matplotlib`, `seaborn`.
    ```bash
    pip install numpy pandas matplotlib seaborn
    ```
2.  Run the script from your terminal:
    ```bash
    python your_script_name.py
    ```
The script will execute the full experiment, print a detailed analysis to the console, and save the visualization plots as `ashrae_full_experiment_results.png`.

## Conclusion

This project moves beyond theoretical discussions of AI bias and provides a concrete, quantifiable demonstration of both the problem and a viable solution. The failure of the Biased agent and the success of the Fairness-Aware agent underscore a critical lesson for the future of AI development: if we don't consciously and explicitly design our systems for fairness, we risk building a future that is inequitable by default. By prioritizing fairness alongside accuracy, we can create AI systems that are not only more effective but also more just.
