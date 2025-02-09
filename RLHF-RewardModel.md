<h1>Reward model</h1>

# Overview
The concept of alignment is crucial for enhancing the performance of language models. Alignment involves optimizing an AI system’s behavior to reflect both the designers' intentions and user expectations [1-5]. In the realm of large language models, this concept is realized through Reinforcement Learning from Human Feedback (RLHF), which enables the model to generalize more effectively [6-7]. RLHF consists of two primary stages: the first involves gathering preference data from a diverse set of crowdsource workers to train a reward model, while the second employs reinforcement learning to refine the language model to maximize this reward.

However, reward models face several significant challenges. Firstly, the input data used to train these models often contains noise, including disagreement, incorrect preferences, and ambiguity. Human decision-making is inherently noisy, which can obscure the true underlying preferences and affect the reward model's performance. Addressing this noise is essential for improving the effectiveness of the reward model. Secondly, reward models typically struggle with generalization. A model trained on a specific set of examples may perform poorly when encountering out-of-distribution data [10]. These limitations can introduce instability into the reinforcement learning process and increase the overhead costs associated with iterative RLHF when new preference data emerges.

To enhance the performance of reward models, a novel architecture incorporating unsupervised contrastive loss has been developed. This advancement allows the model to more effectively discern subtle differences in preferences among responses. Additionally, the new architecture improves the model's ability to differentiate between outputs in the target domain. It achieves this by leveraging multiple components, each trained on distinct distribution preference data, which can then be transferred to handle out-of-domain scenarios more effectively.

# Reward model

The reward model is a crucial component of the RLHF process. The RLHF pipeline typically involves three phases. The first phase is supervised fine-tuning, which begins with a generic pre-trained language model and involves fine-tuning it on a high-quality dataset tailored for specific downstream tasks. The second phase involves preference sampling and the training of the reward model. In the final phase, the reinforcement learning approach, specifically proximal policy optimization [16], is employed to fine-tune the model. This phase uses the reward function to provide feedback to the language model, aiming to maximize the reward objective. KL-divergence is utilized in this context to preserve diversity by acting as an entropy bonus and ensuring that the reinforcement learning policy's outputs remain within the distribution where the reward model is most accurate [18].

During the second phase, the fine-tuned model generates two distinct outputs in response to a user query. Human labelers then select the preferred output, rejecting the other. Methods such as the Bradley-Terry model can be used to compute a preference distribution based on this feedback, employing a reward function to guide the process. Treating this task as a binary classification problem results in the use of a negative log-likelihood loss function to optimize the reward model.

 
# Improve reward model performance
Three techniques are used to improve the performance of the rewuard model: flipping noise data labels, apply label smothning, and employ adaptive margin.

# Contrastive learning for reward modeling
