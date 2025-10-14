# AI Model


| Model            | Bedrock Availability | Accuracy   | Strengths                          | Weaknesses                                  | Improvement Strategy                                                                 |
|------------------|----------------------|------------|------------------------------------|---------------------------------------------|--------------------------------------------------------------------------------------|
| **LLaVA**        | No (Google Colab)    | ~30%       | Detailed outputs, contextual       | Very low disease accuracy                    | Fine-tune on a strawberry disease dataset (white/grey/black mould) using LoRA; add pre-processing filters for color correction |
| **Amazon Nova**  | Yes                  | ~30–35%    | Contextual reasoning attempts      | Poor fruit & disease detection               | Train with fruit detection bounding boxes; integrate pre-trained object detection (YOLOv8/Faster R-CNN) before passing crops to Nova |
| **Claude 3**     | Yes                  | —          | Consistent context detection       | Confusion between bruise vs. disease         | Provide prompt engineering with step-by-step reasoning + fine-tune with labeled disease vs bruise datasets |
| **Pixtral (Mistral)** | Yes             | ~50–60%    | Best anomaly detection, mould awareness | Confused between similar colors of fungi | Add color-normalization pre-processing (remove lighting variance); fine-tune on labelled strawberry disease images |


# Plant Disease Detection Lambda

This AWS Lambda function automatically analyzes plant images uploaded to an S3 bucket, uses **Amazon Bedrock (Pixtral model)** to identify possible diseases, and stores the diagnostic results in Amazon DynamoDB.

## Architecture

1. S3 Trigger: When a plant image is uploaded, the Lambda function runs.
2. Lambda Function: 
   - Downloads the image from S3  
   - Sends it to Amazon Bedrock for visual analysis  
   - Parses the model output (JSON)  
   - Saves results to DynamoDB  
3. DynamoDB: Stores the results (disease name, health status, confidence score, etc.)

