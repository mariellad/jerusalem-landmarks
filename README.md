# Automated Landmark Detection of Historical Photographs of Jerusalem from the Library of Congress online collection

## Introduction
This project aims to develop an automated methodology for detecting landmarks in photographs. This approach is initially applied to a collection from the Library of Congress featuring images of Jerusalem, with the potential to be adapted for other photographic collections.

## Methodology
![Methodology Flowchart](/images/methodology_flowchart.png)
### Landmark Query
- **Initial Query**: Images are sourced from the Library of Congress website using 'Jerusalem' as a keyword, yielding 16,476 images.
- **Landmark List**: A list of 202 Jerusalem landmarks (with multiple denominations and languages) is compiled. Each landmark name is queried individually on the Library of Congress website to gather image URLs.
- **Comparison**: The URLs from individual landmark queries are compared with the total list from the 'Jerusalem' query to identify unique image URLs. This allows for the calculation of the percentage of images with pre-identified landmarks.
- the code to perform landmark query is listed in get_url_queries.ipynb.

### Detection using OpenAI API Models
- **Image Selection**: 300 images are randomly selected from the total collection.
- **Model Selection**: Three OpenAI API models are used:
  1. **GPT-3.5-turbo-1106**: Most capable and cost-effective in the GPT-3.5 family: [gpt-api/gpt-3.5.ipynb] (gpt-3.5.ipynb)
  2. **GPT-4-1106-preview**: Latest GPT-4 model with improved instruction following: [gpt-api/gpt-4_metadata.ipynb] (gpt-4_metadata.ipynb)
  3. **GPT-4-vision-preview**: Capable of handling and reading images directly: [gpt-api/gpt4-vision.ipynb](gpt4-vision.ipynb)
- **Metadata Processing**: Only metadata (image id, description, location, notes, etc.) is provided to the first two models, due to their inability to process images directly.
- **Batch Processing**: Images are processed in batches of 20, with a 15-minute interval between batches to adhere to rate limits.

## Evaluation
- **Ground Truth Establishment**: A ground truth is established for the selected images.
- **Model Comparison**: Outputs from each model are compared to the ground truth using fuzzy matching (Levenstein distance). The model with the highest average score is selected.
- The code for evaluation is in evaluation.ipynb.

## Scaling Up
- **Expanded Processing**: The selected model is rerun with a larger set of approximately 1,000 images.
- **Data Storage**: Structured results are saved in a `.txt` file for further processing.

