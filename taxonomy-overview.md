---

copyright:
  years: 2025, 2025
lastupdated: "2025-04-17"

keywords: instructlab, taxonomy, knowledge, skills, leaf node, branch, qna, files, documents

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}

# How taxonomies are structured for {{site.data.keyword.short_name}}
{: #taxonomy-overview}

A taxonomy is a file directory that consists of the data you feed to the model. It is organized in a cascading structure where each sub-directory, or "branch", of the taxonomy "tree" ends with a "leaf node", which is a set of files that contain the relevant data. You can contribute to a taxonomy by adding an entirely new "branch", or by adding new data to an existing `qna.yaml` file. For more information on the taxonomy structure, see [About the InstructLab Taxonomy](https://docs.instructlab.ai/taxonomy/){: external} in the InstructLab docs. You can also view the [InstructLab taxonomy on GitHub](https://github.com/instructlab/taxonomy){: external}.

For steps on creating or adding to a taxonomy, see [Preparing taxonomies](/docs/instructlab?topic=instructlab-taxonomy-prep).

## Taxonomy data
{: #taxonomy-data}

There are three categories of data in the taxonomy.

Knowledge
:   Data and facts that are supported by sources such as textbooks or encyclopedias. When you add knowledge to a taxonomy, you must reference a separate *knowledge document* that exists outside of the taxonomy directory and acts as a source of truth.

Foundational skills
:   Basic skills such as math, language, and programming that can be used to for acquiring more knowledge. These skills are usually developed using public data.

Compositional skills
:   Skills that combine knowledge and foundational skills to complete more complex tasks, such as stock market analysis.

For more information on the categories, see [What is a "skill"?](https://docs.instructlab.ai/taxonomy/skills/){: external} and [What is "knowledge"?](https://docs.instructlab.ai/taxonomy/knowledge/){: external} in the InstructLab docs. 

## Taxonomy files
{: #taxonomy-files}

There are two types of data files required for each "leaf node".

`qna.yaml`
:   Includes questions and answers relevant to the information found in the knowledge document. Questions and answers are organized as key/value pairs. 

`attribution.txt`
:   Includes sources for the information added to the `qna.yaml` file. This is optional, but is required for contributions to the open-source InstructLab taxonomy repository.

## Knowledge documents
{: #knowledge-docs}

Any knowledge added to a taxonomy must be backed up by a knowledge document, which acts as a source of truth for the information fed to the model. The document must be a Markdown file that exists in a directory separate from the taxonomy. You reference the knowledge document and the directory where it is stored in the `document_outline` section of the `qna.yaml` file. For more information and samples of a knowledge document, see [Preparing your knowledge documents](https://docs.instructlab.ai/taxonomy/upstream/knowledge_contribution_details/#preparing-your-knowledge-documents){: external} and [Example of a knowledge document file](https://github.com/instructlab/taxonomy?tab=readme-ov-file#knowledge-markdown-file-example) in the InstructLab documentation.

## Knowledge `qna.yaml` files
{: #knowledge-qna}

The knowledge `qna.yaml` file includes questions and answers based on the information found in the relevant knowledge document. Questions and answers are stored as key/value pairs, and a minimum of five pairs is required for each `qna.yaml` file. At the bottom of your `qna.yaml` file in the `document_outline` section, you must reference the knowledge document and the directory where it is stored. For the full `qna.yaml` file requirements and examples of knowledge contributions, see [The knowledge files](https://docs.instructlab.ai/taxonomy/knowledge/file_structure/#the-knowledge-files){: external} and [Example of a knowledge submission](https://docs.instructlab.ai/taxonomy/knowledge/file_structure/#example-of-a-knowledge-submission){: external} in the InstructLab documentation. 

## Skills `qna.yaml` files
{: #skills-qna}

The skills `qna.yaml` contains questions and answers that teach a simple task. To teach a model to rhyme, for example, you might include a question such as `What are 5 words that rhyme with skill?` with the answer `spill, mill, drill, fill, chill`. Questions and answers are stored as key/value pairs, and a minimum of five pairs is required for each `qna.yaml` file.

The skills you add can be grounded, meaning they require additional inputs to add context, or ungrounded, meaning they do not require any additional context. For grounded skills, you add context in the `qna.yaml` file with the `context` field. When you add a grounded skill to a taxonomy, it must be on a branch that begins with the word `grounded`, such as `grounded/games/sudoku`.

For the full `qna.yaml` requirements and examples of skills contributions, see [The skills files](https://docs.instructlab.ai/taxonomy/skills/file_structure/#the-skills-files){: external} in the InstructLab documentation. Note that you do not need to add a separate document when adding skills. 
