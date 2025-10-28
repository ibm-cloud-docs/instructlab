---

copyright:
  years: 2024, 2025
lastupdated: "2025-10-28"

keywords: instructlab, ai, about, how it works, billing

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}


# About {{site.data.keyword.instructlab_full_notm}}
{: #about}

{{site.data.keyword.instructlab_full}} is a business-ready, private, and secure generative AI solution for enhancing **large language models (LLMS)**, powered by Red Hat Enterprise Linux AI. An open source project created by IBM and Red Hat, {{site.data.keyword.short_name}} is a cost-effective entry point into the world of [machine learning](#x8397498){: term}, allowing you to make contributions to an LLM without having to own and operate hardware infrastructure. 
{: shortdesc}

You start by providing knowledge and skills that matter most to your business in what's known as a **taxonomy**, or a directory of data. The taxonomy is used to generate **synthetic data**, which is then used to train the model through multiple phases of **fine-tuning**. This process aligns your LLM with your goals by providing not just general knowledge, but the specific skills and contexts that are most important for your unique business needs.

[Learn more about InstructLab](https://www.redhat.com/en/topics/ai/what-is-instructlab#red-hat-enterprise-linux-ai){: external}.


### What are large language models?
{: #llm}

Large language models, or LLMs, are AI models that utilize machine learning techniques to generate human language. They are initially trained on large amounts of general data that allow them to understand and generate natural language, then later fine-tuned to align with more specific contexts. For example, a model trained on a large set of general knowledge can later be fine-tuned using data related to a retail business in order to create a customer service chat bot. You can fine-tune LLMs for a wide variety of uses, such as drafting emails, summarizing long bodies of text into a desired format, or finding errors in code. InstructLab provides a platform for training, fine-tuning and then later evaluating LLMs. 

While LLMs can streamline processes in a variety of ways, keep in mind that there are some limitations to what they are capable of. LLMs work with the data they are supplied with. You wouldn't be able to ask an LLM for your birthday, for instance, because your personal information is not part of the training data. Likewise, an LLM on it's own wouldn't be the best option for predicting the future of a stock, in which case it would be more appropriate to use a forecasting model. Additionally, LLMs on their own are static and incapable of interacting with the environment. Tasks such as telling the time or date, for example, would require additional agenetic flows or frameworks. 

For a more detailed explanation of LLMs and how they work, see [What are LLMs?](https://www.ibm.com/think/topics/large-language-models){: external}.

## How it works
{: #howitworks}

Learn about using InstructLab.



Step 1. Provide a taxonomy
:   A taxonomy is a directory of diverse, human-curated data used to train an LLM. The data contains examples of new knowledge and skills for the model to learn from. You can use and contribute to an existing taxonomy, or you can create your own. For more information, see [How taxonomies are structured for {{site.data.keyword.short_name}}](/docs/instructlab?topic=instructlab-taxonomy-overview).

Step 2. Generate synthetic data
:    The information in the taxonomy is used to generate synthetic data that augments the human-provided knowledge and is used to fine-tune the model. [Learn more about the data generation process from Red Hat](https://www.redhat.com/en/blog/how-instructlabs-synthetic-data-generation-enhances-llms){: external}.

Step 3. Train the model
:    The synthetic data is used to train the model in two phases: knowledge tuning and skills tuning. Knowledge tuning is training that focuses on improving the LLM's based knowledge of essential skills. Skill tuning trains the model on more specific skills required for it's intended purpose, such as responding to customer inquiries or analyzing weather trends.




### Why {{site.data.keyword.instructlab_short}}?
{: #benefits}

Learn about some of the benefits of using {{site.data.keyword.instructlab_short}}.

Retain ownership of both the data and the model
:   You control your data and your model. You can choose to use them in the cloud, on-premises, or anywhere else your business requires. Leverage unique business data to unlock efficiencies and drive innovation by creating AI-powered solutions. 

Minimize the risk of catastrophic forgetting
:   For higher accuracy and less risk, built-in Granite models are used as a foundation for learning new skills and knowledge. Previously learned information is not lost when the models learn new information.

Secure, up-to-date, and available
:   Because {{site.data.keyword.instructlab_short}} is available as a service on {{site.data.keyword.cloud}}, you can reduce unnecessary costs by paying just for what you need. Optimize IT expenditures by delivering simpler, faster, and more economical models.


### Resources for learning more
{: #resources}

See what others have to say about InstructLab. 

- [What is InstructLab?](https://www.redhat.com/en/topics/ai/what-is-instructlab){: external}.
- [InstructLab](https://www.ibm.com/think/topics/instructlab?mhsrc=ibmsearch_a&mhq=instructlab){: external}.
- [What is InstructLab and why do developers need it?](https://developer.ibm.com/articles/awb-instructlab-why-developers-need-it/){: external}
- [What is a large language model?](https://www.redhat.com/en/topics/ai/what-are-large-language-models){: external}


## How does billing work?
{: #billing}

To learn more about billing, see the [FAQ](/docs/{{site.data.keyword.subcollection}}?topic={{site.data.keyword.subcollection}}-faq#costs).
