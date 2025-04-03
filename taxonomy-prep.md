
---

copyright:
  years: 2025, 2025
lastupdated: "2025-04-03"

keywords: instructlab, taxonomy, prepare, create taxonomy, qna, knowledge document, documents

subcollection: instructlab

---

# Preparing taxonomies
{: #taxonomy-prep}

Follow these steps to create your own taxonomy. For more information on taxonomies and the data they include, see [How taxonomies are structured](/docs/instructlab?topic=instructlab-taxonomy-about).
{: shortdesc}

## Create or clone your taxonomy
{: #taxonomy-create}
{: step}

You can [fork and clone the existing InstructLab community taxonomy](https://github.com/instructlab/taxonomy){: external}, or you can create a new taxonomy from scratch in your own GitHub repo. For examples and diagrams showing how you can structure your own taxonomy, see [Upstream taxonomy tree layout](https://docs.instructlab.ai/taxonomy/#upstream-taxonomy-tree-layout){: external} in the InstructLab docs. 

## Gather your knowledge documents
{: #taxonomy-gather}
{: step}

Format your knowledge documents as a Markdown `.md` file and store them in a directory that is separate from the taxonomy. For an example of a knowledge document, see the [InstructLab documentation](https://docs.instructlab.ai/taxonomy/knowledge/file_structure/#example-of-a-knowledge-document-file){: external}. 

Knowledge documents are only required when adding knowledge to your taxonomy, not skills. For more information on the difference between knowledge and skills see [Taxonomy data](/docs/instructlab?topic=instructlab-taxonomies-about#taxonomy-data).
{: note}

## Create `qna.yaml` files for knowledge and skills
{: #taxonomy-qna}

1. Create a `qna.yaml` file that includes questions and answers related to the knowledge or skill you want to add. The file must have at least 5 question and answer pairs and must follow standard YAML formatting. For a complete list of fields required for the `qna.yaml` file, see the InstructLab docs for adding [knowledge](https://docs.instructlab.ai/taxonomy/knowledge/file_structure/#the-knowledge-files){: external} or [skills](https://docs.instructlab.ai/taxonomy/skills/file_structure/#the-structure-of-the-qnayaml-file){: external}. 

2. If you are creating a `qna.yaml` file for a knowledge addition, you must reference the relevant knowledge document, the commit hash for the document, and the directory where it is stored in the `document` section of the file. 

  Example knowledge document and directory reference.

  ```yaml
  document:
      repo: https://github.com/user/my_knowledge
      commit: 0a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9u
      patterns:
        - knowledge_document.md
  ```
  {: screen}

3. Add the file to the correct node in your taxonomy. 

In addition to creating a new `qna.yaml` file, you can also add question and answer pairs to existing files. 
{: tip}

## Upload your taxonomy to your COS bucket
{: #taxonomy-upload}
{: step}

Use the [UI](/docs-draft/instructlab?topic=instructlab-getting-started&interface=ui#taxonomy-add-ui) or the [CLI](https://test.cloud.ibm.com/docs-draft/instructlab?topic=instructlab-getting-started&interface=cli#taxonomy-add-ui) to upload and store your taxonomy to your COS bucket. 

## What's next?
{: #taxonomy-next}

Learn how to [generate data from your taxonomy](/docs-draft/instructlab?topic=instructlab-data-generate&interface=ui). 
